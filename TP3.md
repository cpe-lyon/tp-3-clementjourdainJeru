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

1.  Pour observer les droits sur le dossier et le fichier créés, on fait `stat -c %A test` avec rwxrwxr-x comme droits, et `stat -c %A test/fichier` avec rw-rw-r-- comme droits
2.  On retire tous nos droits sur le fichier avec la commande `chmod 000 fichier`, ce qui le rend inaccessible sauf pour le superadministrateur root, car il possède tous les droits
3.  On se réatribue les droits e tant que root avec `chmod 333 fichier` pour n'avoir que le write et l'execute. L'application de la commande est alors bien effective sur le fichier cependant n'ayant pas les droits de lecture on ne peut le voir qu'en utilisateur root.
4.  Compte tenu que l'on s'est donné les droits d'execution, nous pouvons le faire tout comme sudo qui possède tous les droits
5.  On se retire les droitsd e lecture du dossier test avec la commande `chmod 333 /home/User/test`. En nous retirant les droits de lecture on ne peut plus lister le contenu du dossier test mais on peut toujours modifier le fichier.
6.  En modifiant nos droits sur le fichier nouveau avec `chmod 555 nouveau`, on ne peut lpus le modifier. En nous redonnat les droit sur le dossier test, on en peut toujours pas modifier le fichier nouveau mais on peut le supprimer
7.  On se retire nos droits d'execution sur test avec `chmod 666 test`. On ne peut alors plus rentrer dans le dossier test ni créer de nouveaux fichiers, on peut cependant lister les fichiers et dossiers mais sans y accéder
8.  En s'enlevant de nouveau les droits d'execution au sein du dossier test, on ne peut plus rien faire, même lister les fichiers et dossiers présents. On peut cependant retourner au répertoire précédent, ce qui nous prive de retourner dans le dossier test. Cela implique donc que le droit d'execution sur le dossier courant est essentiel pour toute action entreprise au sein de ce dossier
9.  Pour attribuer des droits à un memebre du groupe pour pouvoir lire mais pas modifier le fichier fichier , il faut taper `chmod 755 fichier` ou `chmod 745 fichier`
10. Pour créer un umask extrêmement restrictif pour tous les autres utilisateurs, il faut taper `umask 077`
11. Pour créer un umsk très permissif pour les autres sauf pour écrire, il faut taper `umask 022`
12. Pour m'autoriser un accès complet et un accès qu'à mes membres du groupe en lecture, il faut taper `umassk 037`
13. -`chmod u=rx,g=wx,o=r fic` = `chmod 534 fic` // `chmod uo+w,g-rx fic`= `chmod 652 fic` // `chmod 653 fic` = `chmod u=rw g+r o+w fic` // chmod u+x,g=w,o-r fic = `chmod 520 fic`
14. Le fichier etc/ passwd peut être lu par tous mais ne peut être modifié que par nous l'utilisateur, tandis que les droits sur le programmes sont de le lire et de l'executer pour les autres utilisateurs
