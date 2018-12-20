# B1 Réseau 2018 - Thibault Feugère


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

**A quoi sert la gateway dans le réseau d'Ingésup ?**

Le gateway est l'adresse qui permet de communiquer avec internet.

**Calculez la première et la dernière IP disponibles du réseau :**

La première adresse IP disponible est `10.33.3.1`
La dernière adresse IP disponible est `10.33.3.255`

**Nmap :**

Aprés l'installation de Nmap, j'ai tapé la commande `nmap -sn -PE 10.33.0.0/22`

>Nmap done: 1024 IP addresses (378 hosts up) scanned in 52.79 seconds

`MAC Address: 44:03:2C:2C:BD:5C (Intel Corporate)`

`Nmap scan report for 10.33.3.239`

`Host is up (0.091s latency).`

`MAC Address: F4:BF:80:C0:A5:8A (Unknown)`

`Nmap scan report for 10.33.3.242`

On remarque qu'il y a des adresses IP disponibles entre `10.33.3.239` et `10.33.3.242`.

Par exemple, `10.33.3.240` est libre. On peut donc s'attribuer cette adresse IP en utilisant la méthode graphique expliquée ci-dessus.

## II. Exploration locale en duo

### 1. Prérequis 
+ On a un cable RJ45
+ On a deux PC
+ On a désactivé nos deux firewalls

### 2. Cablâge

C'est fait, branché via le port Ethernet à nos cartes Ethernet

### 3. Modification d'adresse IP

Nous avons tout deux modifié l'adresse IP de notre carte Ethernet

Adresse IP de Thibault : 10.0.0.2
Adresse IP de MAxime : 10.0.0.3 
Masque de sous-réseau : `255.255.255.0`

**Test avec le ping :**

`PS C:\Users\Thibault> ping 10.0.0.3

Envoi d’une requête 'Ping'  10.0.0.3 avec 32 octets de données :
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64
Réponse de 10.0.0.3 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.0.0.3:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms`