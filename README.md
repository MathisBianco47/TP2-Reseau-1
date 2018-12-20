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
   + Clic droit sur le réseau souhaité (*Ici c'est WIFI@YNOV)
   + Clic gauche sur *Statut*
   + Clicl gauche sur *Détail*