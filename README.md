# Checkpoint-2
Q.1.1 le ping avec les adresses IP des machines ne fonctionnent pas parceque :
- Problèmes de pare-feu : Les pare-feu peuvent bloquer les requêtes ping. 

- Problèmes de configuration réseau : les adresses IP et les masques de sous-réseau sont correctement configurés sur les machines.

 -  Vérification coté serveur:
[![pingMarchePas](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePas.png)

 -  Vérification coté serveur:
   [![pingMarchePasCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarchePasCoteServeur.png)



Q.1.3 Modifie la configuration réseau du client pour qu'il soit en DHCP.
j'ai modifié le paramétrage DHCP sur le client
[![DHCP_auto](https://github.com/fcisse-c/Checkpoint-2/blob/main/DHCP_auto.png)

Le client ne récupère pas la 1ère adresse disponible sur la plage DHCP du serveur  carCertaines adresses IP dans la plage DHCP peuvent être réservées pour des appareils spécifiques ou exclues de la distribution. Cela peut empêcher le client de récupérer la première adresse disponible
[![IP_avDHCP](https://github.com/fcisse-c/Checkpoint-2/blob/main/IP_avDHCP.png)


- Ping coté serveur:
[![pingMarcheCoteServeur](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteServeur.png)


- Ping coté client:
[![pingMarcheCoteClient](https://github.com/fcisse-c/Checkpoint-2/blob/main/pingMarcheCoteClient.png)
