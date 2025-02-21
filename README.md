# Checkpoint-2
Q.1.1 le ping avec les adresses IP des machines ne fonctionnent pas parceque :
- Problèmes de pare-feu : Les pare-feu peuvent bloquer les requêtes ping. 

- Problèmes de configuration réseau : les adresses IP et les masques de sous-réseau sont correctement configurés sur les machines.

 -  Vérification coté serveur:
[![pingMarchePas](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePas.png)

 -  Vérification coté serveur:
   [![pingMarchePasCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePasCoteServeur.png)

# Exercice :  Modification IP client serveur 

Q.1.3 Modifie la configuration réseau du client pour qu'il soit en DHCP.
j'ai modifié le paramétrage DHCP sur le client
[![DHCP_auto](https://github.com/fcisse-c/Checkpoint-2/blob/main/DHCP_auto.png)

Le client ne récupère pas la 1ère adresse disponible sur la plage DHCP du serveur  carCertaines adresses IP dans la plage DHCP peuvent être réservées pour des appareils spécifiques ou exclues de la distribution. Cela peut empêcher le client de récupérer la première adresse disponible

[![IP_avDHCP](https://github.com/fcisse-c/Checkpoint-2/blob/main/IP_avDHCP.png)


- Ping coté serveur:
- 
[![pingMarcheCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteServeur.png)


- Ping coté client:
  
[![pingMarcheCoteClient](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteClient.png)

Q.1.4 Oui le client peut avoir l'adresse IP 172.16.10.15 en DHCP 
Voici les manipulations à faire :

[![creation_reservation](https://github.com/fcisse-c/Checkpoint-2/blob/main/creation_reservation.png)

J'ai Configuré le client pour utiliser DHCP  en Ouvrant l'invite de commandes et tapant ipconfig /release suivi de ipconfig /renew pour obtenir une nouvelle adresse IP du serveur DHCP.

[![IPconfig_re](https://github.com/fcisse-c/Checkpoint-2/blob/main/IPconfig_re.png)

ipconfig /all sur le client:

[![IPconfig_all](https://github.com/fcisse-c/Checkpoint-2/blob/main/IPconfig_all.png)


# Exercice 2 : Débogage de script PowerShell 

Exercice 3 : Vérification d'une infrastructure réseau

Q.3.1 Quel est le matériel réseau A ?
Le matériel réseau A est un switch (commutateur).

Son rôle vis-à-vis des ordinateurs :
Il connecte les ordinateurs (PC1 à PC5) dans un réseau local (LAN).
Il permet la communication entre les PC en transmettant les données uniquement vers le port où se trouve la machine destinataire (grâce aux adresses MAC).
Il travaille principalement sur la couche 2 (liaison de données) du modèle OSI.

Q.3.2 Quel est le matériel réseau B ?
Le matériel réseau B est un routeur.

Son rôle pour le réseau 10.10.0.0/16 :
Il connecte le réseau local (10.10.0.0/16) aux réseaux extérieurs (par exemple, 172.16.5.0/24 via R2).
Il effectue le routage des paquets en choisissant le meilleur chemin pour atteindre un réseau de destination.
Il fonctionne sur la couche 3 (réseau) du modèle OSI en utilisant les adresses IP.
Il gère la passerelle par défaut pour permettre la communication inter-réseaux.

Q.3.3 Que signifie f0/0 et g1/0 sur l’élément B ?
Ce sont des noms d'interfaces réseau sur le routeur :

f0/0 :

f signifie FastEthernet, une interface Ethernet avec un débit de 100 Mbps.
0/0 indique la position du port : module 0, port 0.
g1/0 :

g signifie GigabitEthernet, une interface Ethernet avec un débit de 1 Gbps.
1/0 indique le module 1, port 0.
Ces interfaces permettent au routeur de connecter différents réseaux physiques ou logiques.

Q.3.4 Pour l'ordinateur PC2, que représente /16 dans son adresse IP ?
PC2 a l’adresse 10.11.80.2/16.

Le /16 est la notation CIDR (Classless Inter-Domain Routing), qui indique la longueur du masque de sous-réseau.
/16 signifie que les 16 premiers bits de l’adresse IP représentent la partie réseau.
En notation décimale, cela correspond à un masque :
255.255.0.0

Cela implique que tous les appareils dont les 16 premiers bits de l’adresse IP sont identiques (ici 10.11.x.x) appartiennent au même sous-réseau.

Q.3.5 Pour ce même ordinateur, que représente l'adresse 10.10.255.254 ?
L’adresse 10.10.255.254 représente la passerelle par défaut (default gateway) de PC2.

Rôle de la passerelle par défaut :
C’est l’adresse IP du routeur (B) sur le réseau local.
Elle permet à PC2 d’envoyer des paquets vers d’autres réseaux, notamment Internet ou d’autres sous-réseaux (comme 172.16.5.0/24).
Lorsque PC2 veut communiquer avec une adresse IP en dehors de son réseau (10.11.0.0/16), il transmet ses paquets à cette adresse, et le routeur se charge du routage vers la destination appropriée.

