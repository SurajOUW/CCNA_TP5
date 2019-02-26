# CCNA_TP5
Initiation à Cisco

_____________________________________________

# TP 5

## Premier pas Cisco (avec le logiciel GNS3)

# I Préparation des VMs

On clone la vm patron (centos) à trois reprises pour avoir un serveur et 2 "clients"

Tout d'abord on organise la topologie du réseau que l'on va faire grâce à GNS3

https://i.postimg.cc/ZYs3D3c9/Screenshot-1.png
(avant que l'on allume)

Une fois les routes correctement agencé on vérifie que les VM soient bien éteintes et on les allumes avec GNS3

https://i.postimg.cc/nV6DKx2g/Screenshot-2.png

Les VM sont correctement relié entre elles.
On les fermes à nouveau puis on va configurer les routeurs (double clic dessus pour ouvrir Solar putty)

## II Lancement et configuration du lab

__!!! La première ligne de chaques paragraphes de commandes contient un point pour pas que la commande # conf t soit affiché en majuscule à cause du format .md ne pas en tenir compte s'il vous plaîîît !!!__
````
.# conf t
(config)# interface ethernet 0/1
(config-if)# ip address 10.5.1.254 255.255.255.0
(config-if)# no shut
__la route entre R1 et le serveur__

.# conf t
(config)# interface ethernet 0/0
(config-if)# ip address 10.5.3.1 255.255.255.254
(config-if)# no shut
__la route entre R1 et R2__

.# conf t
(config)# interface ethernet 0/0
(config-if)# ip address 10.5.3.2 255.255.255.254
(config-if)# no shut
__la route entre R2 et R1__

.# conf t
(config)# interface ethernet 0/1
(config-if)# ip address 10.5.2.254 255.255.255.0
(config-if)# no shut
__la route entre R2 et le switch__
````
* On vérifie que les routes soient correctes : 

-Serveur 1 : 
-- Route : 10.5.2.0/24 via 10.5.1.254 dev enp0s3

-Routeur 1 : 
-- Route : ip route 10.5.2.0 255.255.255.0 10.5.3.2

-Routeur 2 : 
-- Route : ip route 10.5.1.0 255.255.255.0 10.5.3.1

-Client 1 : 
-- Route : 10.5.1.0/24 via 10.5.2.254 dev enp0s3

-Client 2 : 
-- Route : 10.5.1.0/24 via 10.5.2.254 dev enp0s3

## III DHCP
