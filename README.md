# B1 Réseau 2018 - Thibault Feugère

*N.B : Désolé, nous savons que tu n'aimes pas les screenshots mais nous t'en avons mis deux car nous n'avons pas trouvé d'alternatives. Bonne lecture.*

Maxime Larrieu : 
![alt text](https://github.com/flamingfurry/TP2-Reseau/blob/master/maxime.jpg "Photo de Maxime")

Thibault Feugère : 
![alt text][logo]

[logo]: https://github.com/flamingfurry/TP2-Reseau/blob/master/thibault.png "Photo de Thibault"

## I. Exploration locale en solo


### 1. Affichage d'informations sur la pile TCP/IP locale


---
**Affichez les infos des cartes réseau de votre PC :**

J'ouvre le Powershell et je lance la commande `ipconfig /all`


| NOM         | Carte Réseau Sans Fil           | Binaire|
| ------------- |-------------|----------------|
| Masque de sous-réseau      | 255.255.252.0 | 11111111.11111111.11111100.00000000|
| Adresse MAC      | 20-16-B9-E9-7D-E8      ||
| Adresse IP (IPv4) | 10.33.2.92 (préféré)      | 00001010.00100001.00000010.01011100 |


| NOM         | Carte Ethernet Ethernet |
| ------------- |-------------|
| Adresse MAC      | 10-65-30-74-17-F0      |
| Adresse IP      | il n'y en a pas car c'est relié à un port RJ45|


Adresse de réseau de la carte WiFi : `10.33.0.0`

Adresse de broadcast de la carte WiFi : `10.33.3.255/22` =>  00001010.00100001.00000011.11111111

---
**Affichez votre gateway**

On peut obtenir ce genre d'informations avec la commande `ipconfig` tout simplement.

Passerelle par défaut : `10.33.3.253`


---
**GUI - Trouvez comment afficher les informations sur une carte IP (change selon l'OS) :**


+ Clic droit sur l'icône *Wifi*, dans le coin bas droit sur W10
   + *Ouvrir les paramètres Réseau et Internet*
+ Clic gauche sur *Centre Réseau et Partage*
+ Clic gauche sur *Modifier les paramètres de la carte*
   + Clic droit sur le réseau souhaité (Ici c'est *WIFI@YNOV*)
   + Clic gauche sur *Statut*
   + Clicl gauche sur *Détail*

---
**A quoi sert la gateway dans le réseau d'Ingésup ?**

Le gateway est l'adresse qui permet de communiquer avec internet.

---
**Calculez la première et la dernière IP disponibles du réseau :**

La première adresse IP disponible est `10.33.3.1`
La dernière adresse IP disponible est `10.33.3.255`

---
**Nmap :**

Aprés l'installation de Nmap, j'ai tapé la commande `nmap -sn -PE 10.33.0.0/22`

```
>Nmap done: 1024 IP addresses (378 hosts up) scanned in 52.79 seconds
MAC Address: 44:03:2C:2C:BD:5C (Intel Corporate)
Nmap scan report for 10.33.3.239
Host is up (0.091s latency).
MAC Address: F4:BF:80:C0:A5:8A (Unknown)
Nmap scan report for 10.33.3.242
```

On remarque qu'il y a des adresses IP disponibles entre `10.33.3.239` et `10.33.3.242`.

Par exemple, `10.33.3.240` est libre. On peut donc s'attribuer cette adresse IP en utilisant la méthode graphique expliquée ci-dessus.

---

## II. Exploration locale en duo

### 1. Prérequis


+ On a un cable RJ45
+ On a deux PC
+ On a désactivé nos deux firewalls


### 2. Cablâge


C'est fait, branché via le port Ethernet à nos cartes Ethernet

---

### 3. Modification d'adresse IP


Nous avons tout deux modifié l'adresse IP de notre carte Ethernet

Adresse IP de Thibault : `10.0.0.2`

Adresse IP de Maxime : `10.0.0.3`

Masque de sous-réseau : `255.255.255.0`

---

**Test avec le ping :**

```
PS C:\Users\Thibault> ping 10.0.0.3
Envoi d’une requête 'Ping'  10.0.0.3 avec 32 octets de données :
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
```


Statistiques Ping pour 10.0.0.3 :

```
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
---

### 4. Utilisation d'un des deux comme gateway

Maxime désactive sa Wifi et n'a plus accès à internet.

J'active, sur ma carte Wifi le partage internet à ma carte ethernet afin de lui partager internet.
Il renseigne manuellement une adresse IP : 192.168.137.8 et utilise mon IP comme passerelle : 192.168.137.1
Il renseigne les DNS de Google 8.8.8.8

Le ping fonctionne :

```
PS C:\Users\Thibault> ping 192.168.137.8
Envoi d’une requête 'Ping'  192.168.137.8 avec 32 octets de données :
Réponse de 192.168.137.8 : octets=32 temps<1ms TTL=64
Réponse de 192.168.137.8 : octets=32 temps<1ms TTL=64
Réponse de 192.168.137.8 : octets=32 temps<1ms TTL=64
Réponse de 192.168.137.8 : octets=32 temps<1ms TTL=64
```

Il a internet !!!

---

### 5. Petit chat privé

Notons qu'à partir d'ici, la suite des tests et du TP a été réalisé sur un Windows, un Fedora mais aussi sur un Mac.

Le PC sous Fedora de Maxime a servit de PC serveur avec pour adresse IP : `192.168.1.36`

Le PC sous Mac de Maxime a servit de PC client.

L'avantage de ces deux OS est que nous n'avions pas besoin d'installer Netcat.

Pour se mettre en PC serveur, Maxime a tapé la commande `nc -l -p 8888`
Pour se connecter au PC serveur de Maxime, j'ai tapé, sur son mac la commande `nc 192.168.1.36 8888`

Maxime Larrieu : 
![alt text](https://github.com/flamingfurry/TP2-Reseau/blob/master/maxime.jpg "Photo de Maxime")

---

### 6. Wireshark

On ne comprends pas tout sur Wireshark mais voilà un screen de Wireshark sur mac, écoutant uniquement les communications ayant pour protocole TCP et nous avons réussi à répérer deux communications entre le mac et le système sous fedora.

!(https://github.com/flamingfurry/TP2-Reseau/blob/master/wireshark.png)

---

### 7. Firewall

NOTHING

## III. Manipulation d'autres outils/protocoles côté client

### DHCP 


Pour savoir ça il faut aller dans l'invite de commande ou le Powershell et taper `ipconfig /all`

`Serveur DHCP . . . . . . . . . . . . . : 10.33.3.254`

Avec cette commande, on peut aussi obtenir la durée de vite du bail DHCP.


```
Bail obtenu. . . . . . . . . . . . . . : lundi 7 janvier 2019 09:00:39
Bail expirant. . . . . . . . . . . . . : lundi 7 janvier 2019 10:30:38
```

---

**Ce que nous avons compris du DHCP**


Après nos recherches, nous savons que le DHCP signifie Dynamic Host Configuration Protocol ou en français le protocole de configuration automatiques des hôtes.

Il est chargé de la configuration automatique des adresses IP d'un réseau informatique. Cela évite à l'utilisateur de tout paramétrer lui-même.

---

**Demandez une nouvelle adresse IP**


Toujours dans notre invité de commande ou dans le terminal, on tape la commande `ipconfig /renew`

---

### DNS


Toujours avec la commande `ipconfig /all`

`Serveur DNS : 10.33.10.20`

---

**Nslookup**

(Fait sur le réseau de Maxime)


```
PS C:\Users\Thibault> nslookup google.com`
Serveur :   bbox.lan
Address:  192.168.1.254

Réponse ne faisant pas autorité :
Nom :    google.com
Addresses:  2a00:1450:4007:80a::200e
         172.217.18.206
```


```
PS C:\Users\Thibault> nslookup ynov.com
Serveur :   bbox.lan
Address:  192.168.1.254

Réponse ne faisant pas autorité :
Nom :    ynov.com
Address:  217.70.184.38
```

Un DNS signifie Domain Name System, c'est ce qui attribue une adresse IP à un nom de domaine.

Ici nous voyons que le nom de domaine ynov.com est lié à l'adresse IP `217.70.184.38`.
Et le nom de domaine google.com est lié à l'adresse IP `172.217.18.206`.

---

**Reverse lookup**


```
PS C:\Users\Thibault> nslookup 78.78.21.21
Serveur :   bbox.lan
Address:  192.168.1.254

Nom :    host-78-78-21-21.mobileonline.telia.com
Address:  78.78.21.21
```


```
PS C:\Users\Thibault> nslookup 92.16.54.88
Serveur :   bbox.lan
Address:  192.168.1.254

Nom :    host-92-16-54-88.as13285.net
Address:  92.16.54.88
```

C'est la même chose que pour le lookup mais dans l'autre sens. C'est-à-dire que `78.78.21.21` est lié au nom de domaine host-78-78-21-21.mobileonline.telia.com

---

### 3. Bonus

**Se renseigner sur les différences entre WiFi et câble**

La WiFi n'a besoin que de deux cartes WiFi pour fonctionner alors que pour Ethernet il faut deux cartes Ethernet.
Le câble a un meilleur débit que la Wifi car il y a très peu de perte.

---

**explorer l'interface d'administration de votre box (chez vous) avec tout ça en tête**

C'est fait via celle de Bouygues Telecom. L'interface est accessible via l'adresse 192.168.1.254, on y retrouve pleins de notions vues pendant les cours tel que l'IP, la Wifi, les ip locales, etc.

---

**sinon, elle sert à quoi la MAC si on a des IP ? => Se renseigner sur ARP**

Une adresse IP est attribuée en fonction du réseau et peut changer alors que l'adresse MAC est physique en fonction de la carte réseau. Autrement dit, l'adresse IP change en fonction des réseaux et l'adresse MAC reste la même.

Nous n'avons pas de switch.

---