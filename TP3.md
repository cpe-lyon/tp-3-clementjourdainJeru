# Exercice 1. Gestion des utilisateurs et des groupes

1.  Pour ajouter les groupes, il faut taper `sudo groupadd dev` et `sudo groupadd infra`
2.  Pour créer des utilisateurs avec un dossier personnel et un shell bash, il faut taper `sudo useradd -m nomutilisateur --shell /bin/bash`
3.  Pour ajouter un utilisateur dans un groupe, il faut taper `sudo adduser nomutilisateur nomgroupe`
4.  Pour afficher les membres d'un groupe on peut soit regarder dans `/etc/group` avec la commande `cat /etc/group` soit avec la commande `grep dev /etc/group`
5.  Pour changre de groupe propriétaire, il faut taper `sudo chgrp nouveaugroupe dossiercible`
6.  Pour changer de groupe primaire, il faut taper `sudo usermod -g nouveaugroupe utilisateur`
7.  En prenant exemple sur le répertoire dev, pour créer un dossier commun aux utilisateurs et leur doner les droits d'écrire dans le dossier, il faut les commandes suivantes : `sudo mkdir /home/dev`, `sudo chgrp dev /home/dev`, `sudo chmod 775 /home/dev`
8.  Pour empêcher la suppression du fichiers des autres dans dans un dossier commun, il faut rajouter le sticky bit avec la commande `chmod 1775 dev`
9.  On ne peut pas se connecter à Alice car il faut créer son mot depasse sinon le compte est inactif
10. Pour activer alice, il faut lui attribuer un mot de passe avec `sudo passwd alice`, puis on vérifie que cela fonctionne avec `su alice`
11. Pour obtenir l'uid et et le gid d'alice, il faut taper `id alice`
12.  Pour retrouver l'utilisateur qui a comme uid 1003, `id 1003`
13.  jsp
14.  Pour trouver le groupe qui a pour gid 1002, `getent group 1002`
15.  On ne peut pas supprimer charlie du groupe infra avec la commande `sudo passwd -d charlie infra` car il s'agit de son groupe primaire
16.  Afin de modifier le compte de dave, il faut écrire `sudo chage dave`et modifier les lignes en fonction
17.  L'interpretru de commande de root est bash
18.  L'utilisateur nobody représente l'utilisateur avec le moins de droits possibles sur linux, et sert afin de faire des tests
19.  La déconnexion par défaut de sudo est de 15 minutes, et pour forcer sudo à oublier notre mot de passe bah jsp

# Exercice 2. Gestion des permissions

1.  `stat -c %A test` avec rwxrwxr-x, `stat -c %A test/fichier` avec rw-rw-r--
2.  
