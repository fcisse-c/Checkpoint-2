# Checkpoint-2

# Exercice 1:  Modification IP client serveur 
Q.1.1 le ping avec les adresses IP des machines ne fonctionnent pas parceque :
- Problèmes de pare-feu : Les pare-feu peuvent bloquer les requêtes ping. 

- Problèmes de configuration réseau : les adresses IP et les masques de sous-réseau sont correctement configurés sur les machines.

 -  Vérification coté serveur:
![pingMarchePas](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePas.png)

 -  Vérification coté serveur:
   [![pingMarchePasCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePasCoteServeur.png)


Q.1.3 Modifie la configuration réseau du client pour qu'il soit en DHCP.
j'ai modifié le paramétrage DHCP sur le client
[![DHCP_auto](https://github.com/fcisse-c/Checkpoint-2/blob/main/DHCP_auto.png)

Le client ne récupère pas la 1ère adresse disponible sur la plage DHCP du serveur  carCertaines adresses IP dans la plage DHCP peuvent être réservées pour des appareils spécifiques ou exclues de la distribution. Cela peut empêcher le client de récupérer la première adresse disponible

![IP_avDHCP](https://github.com/fcisse-c/Checkpoint-2/blob/main/IP_avDHCP.png)


- Ping coté serveur:
- 
![pingMarcheCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteServeur.png)


- Ping coté client:
  
![pingMarcheCoteClient](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteClient.png)

Q.1.4 Oui le client peut avoir l'adresse IP 172.16.10.15 en DHCP 
Voici les manipulations à faire :

![creation_reservation](https://github.com/fcisse-c/Checkpoint-2/blob/main/creation_reservation.png)

J'ai Configuré le client pour utiliser DHCP  en Ouvrant l'invite de commandes et tapant ipconfig /release suivi de ipconfig /renew pour obtenir une nouvelle adresse IP du serveur DHCP.

![IPconfig_re](https://github.com/fcisse-c/Checkpoint-2/blob/main/IPconfig_re.png)

ipconfig /all sur le client:

![IPconfig_all](https://github.com/fcisse-c/Checkpoint-2/blob/main/IPconfig_all.png)


# Exercice 2 : Débogage de script PowerShell 
## Q.2.1 — Exécution de AddLocalUsers.ps1
Problème : Le script AddLocalUsers.ps1 ne s'exécutait pas.
Correction : Utilisation du chemin dans le fichier n'etait pas bon, le bon chemin est "C:\Scripts"

![image](https://github.com/user-attachments/assets/03fedc06-a6fe-432a-b508-4cd7baa4021e)

##  Q.2.2 — Prise en compte du premier utilisateur dans Users.csv
Problème : Le premier utilisateur n'était pas pris en compte.
Correction : Import-Csv lit désormais toutes les lignes, sans sauter la première.

```powershell
Import-Csv -Path $csvPath | ForEach-Object {
    Add-LocalUser -Prenom $_.Prenom -Nom $_.Nom -Description $_.Description
}
```

# Exercice 3 : Vérification d'une infrastructure réseau

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

Q.3.6 Pour les ordinateurs PC1, PC2 et PC5 :

🔹 PC1 : 10.10.4.1/16
Adresse de réseau : 10.10.0.0/16
Première adresse disponible : 10.10.0.1
Dernière adresse disponible : 10.10.255.254
Adresse de diffusion (broadcast) : 10.10.255.255

🔹 PC2 : 10.11.80.2/16
Adresse de réseau : 10.11.0.0/16
Première adresse disponible : 10.11.0.1
Dernière adresse disponible : 10.11.255.254
Adresse de diffusion (broadcast) : 10.11.255.255

🔹 PC5 : 10.10.4.7/15
/15 → Masque : 255.254.0.0
Plage du réseau /15 pour 10.10.x.x : 10.10.0.0 – 10.11.255.255
Adresse de réseau : 10.10.0.0/15
Première adresse disponible : 10.10.0.1
Dernière adresse disponible : 10.11.255.254
Adresse de diffusion (broadcast) : 10.11.255.255

Q.3.7 Quels ordinateurs peuvent communiquer entre eux ?
🔗 Communication directe (sans passerelle) :
Deux hôtes peuvent communiquer directement s'ils appartiennent au même réseau (même adresse réseau + même masque).

PC1 (10.10.4.1/16) et PC5 (10.10.4.7/15) ✔️
✅ Oui, car 10.10.4.1/16 appartient à 10.10.0.0/16, qui est inclus dans 10.10.0.0/15 (PC5).

PC1 et PC2 (10.11.80.2/16) ❌
🚫 Non, car PC1 est dans 10.10.0.0/16 tandis que PC2 est dans 10.11.0.0/16.

PC2 et PC5 ✔️
✅ Oui, car 10.10.0.0/15 englobe les adresses de PC2 et PC5.

PC3 (10.10.80.3/16), PC4 (10.10.4.2/16), PC1 et PC5 ✔️
✅ Oui, tous ces PC partagent des plages compatibles dans le réseau 10.10.0.0/15.
Résumé de la communication directe :
Groupe 1 (peuvent communiquer sans routeur) : PC1, PC3, PC4, PC5
Groupe 2 : PC2 (isolé sans passerelle)

Q.3.8 Qui peut atteindre le réseau 172.16.5.0/24 ?
Pour atteindre un réseau externe (172.16.5.0/24 ici), les PC doivent pouvoir envoyer leurs paquets à la passerelle (10.10.255.254).

Tous les PC peuvent théoriquement atteindre le réseau externe via le routeur B, si leur passerelle par défaut est correctement configurée :
PC1, PC3, PC4, PC5 : ✅ Oui

PC2 : ✅ Oui (malgré qu'il soit dans un sous-réseau différent, le routeur gère l’acheminement inter-sous-réseaux)

Q.3.9 Incidence si on intervertit les ports de connexion de PC2 et PC3 sur le matériel A ?
Le matériel A est un switch, qui fonctionne principalement sur la couche 2 (MAC address).

Conséquences :
Aucune incidence sur la connectivité IP. Les PC conserveront leurs adresses IP et leur appartenance au réseau initial.
Le switch mettra simplement à jour sa table d’adresses MAC pour associer la bonne adresse MAC au bon port.
Conclusion : Pas d’impact sur la communication réseau.

Q.3.10 Configuration IP en dynamique : quelles modifications possibles ?
Si on souhaite une configuration IP dynamique, on utilisera un serveur DHCP (Dynamic Host Configuration Protocol).

Modifications possibles :
Activer un serveur DHCP :

Sur le routeur B ou un serveur dédié.
Configurer des plages d’adresses pour chaque sous-réseau (par exemple, 10.10.0.10 – 10.10.0.100).
Paramétrer les PC en DHCP :

Sur chaque PC : sélectionner “Obtenir une adresse IP automatiquement”.
Configurer les options DHCP :

Passerelle par défaut : 10.10.255.254
DNS : Une adresse DNS publique (par exemple, 8.8.8.8) ou interne.
Durée du bail (lease time) : Durée pendant laquelle l’adresse IP reste attribuée.
Avantages de la configuration dynamique :
Gestion simplifiée des adresses IP.
Réduction des erreurs humaines dans la configuration IP.
Meilleure flexibilité lors de l’ajout ou du déplacement des machines.

