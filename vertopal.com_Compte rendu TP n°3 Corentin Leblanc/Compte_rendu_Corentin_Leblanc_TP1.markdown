**Compte rendu TP 3 -- Utilisateurs, groupes et permissions**

**<ins>Exercice 1. Gestion des utilisateurs et des groupes</ins>**

1 -- Je me suis servi de la commande « **sudo groupadd dev** » et
« **sudo groupadd infra** ». Pour bien vérifier que ces deux groupes ont
été créé je me suis servi de la commande « **cat /etc/group** ».

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image1.png)

2 -- J'ai donc créé 4 utilisateurs avec la commande « **useradd** »
comme il était demandé. J'ai rajouté l'option -m à cette commande de
manière à ce qu'ils aient leur dossier personnel. Plus particulièrement 
"**useradd -m -s /bin/bash nomdel'utilisateur**".

![Une image contenant texte Description générée
automatiquement](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image2.png)

3 -- J'ai ajouté les utilisateurs dans les groupes créées précédemment
comme demandé dans la question.

![Une image contenant texte, tableau de points Description générée
automatiquement](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image3.png)

4 -- Les deux moyens que j'ai trouvés pour afficher les membres du
groupe infra sont :

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image4.png)

Après avoir installé le package « **members** ».

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image5.png)

5 et 6 -- J'ai d'abord changé de groupe primaire pour chaque utilisateur
pour pouvoir ensuite supprimer leur groupe créé précédemment.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image6.png)

Ou par exemple la commande "**chown alice :dev /home/alice**".

![Une image contenant texte Description générée
automatiquement](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image7.png)

Pour remplacez le groupe primaire jai fais "**usermod -g dev alice**".

Puis si je fais un « cat /etc/group », je constate qu'il n'y a plus de
groupes à leurs noms, donc les groupes dev et infra sont bien les
propriétaires des différents répertoires demandés.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image8.png)

7 -- J'ai créée deux répertoires avec la commande « mkdir » puis
modifier les permissions avec la commande « chmod », pour activer les
permissions leur permettant d'écrire je renseigne donc « 755 » en
complément de « chmod ».

« mkdir infra » et « mkdir dev »

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image9.png)

Puis "**chgrp dev /home/dev**" et enfin "**chmod g+w dev**" car c'est root qui a créé le dossier.

8 -- Il faut placer le "sticky bit" avec la commande "**chmod +t dev**" ou "**chmod +t infra**"

La commande serait « chmod 600 nom_du_fichier »

9 -- Non je ne peux pas ouvrir de sessions en tant qu'alice car je n'ai
pas créé de mot de passe pour alice. Par conséquent son compte est
inactif.

10 -- Pour activer le compte d'alice il faut que je lui définisse un mot
de passe.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image11.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image12.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image13.png)

Cela m'a bien demandé un nouveau mot de passe pour le compte d'alice,
ensuite j'ai pu me connecter à son compte.

11 -- Pour obtenir l'uid (Utilisateur ID) et le gid (Groupe ID) j'ai
utilisé la commande « id », on n'obtient donc les résultats suivants.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image14.png)

Pour avoir l'UID "**id -u alice**" et pour le GID "**id -g alice**".

12 -- L'utilisateur disposant de l'uid 1003 est le 3^ème^ utilisateur
qui a été créer, dans mon cas il se trouve que c'est dave. J'ai donc
utilisé la commande « id --u dave » pour retrouver le bon uid.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image15.png)

La commande "**getent passwd 1003 | cut -d :-f1**" permet de retrouver cet utilisateur

13 -- L'ID du groupe « dev » est 1002, j'ai pu trouver le GID du groupe
« dev ».

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image16.png)

On peut trouver l'id du groupe dev grâce à la commande "**grep dev /etc/group | cut -d : -f3**".

14 -- Le groupe qui a pour gid 1002 est le groupe « dev ». (Se référez à
la question précédente.(commande -> "**getent group 1003 | cut -d : -f1**"

15 -- Pour retirer l'utilisateur charlie du groupe « infra » j'ai
utilisé la commande ci-dessous.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image17.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image18.png)

Avec la commande "**gpasswd -d charlie infra**" on aurait pu retirer charlie du groupe infra,
cependant ce n'est pas possible car c'est le groupe primaire de charlie.

16 -- J'ai modifié le compte de dave comme demandé dans la question.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image19.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image20.png)

Voilà le résultat après modification du compte comme demandé. Le compte
expire au 1^er^ juin 2022, il faut changer de mot de passe avant 90
jours, il faut attendre 5 jours pour modifier un mot de passe,
l'utilisateur est averti 14 jours avant l'expiration de son mot de passe
et le compte sera bloqué 30 jours après expiration du mot de passe.
J'aurais également pu me servir de "**sudo chage -E 06/01/2021 -m 5 -M 90 -I 30 -W 14 dave**"

17 -- L'interpréteur de commandes de l'utilisateur nommé « root » est
« /bin/bash ». J'ai pu obtenir ce résultat en faisant un « cat » du
fichier « /etc/passwd ».

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image21.png)

On a vu dans le cours que le dernier champ du fichier /etc/passwd est
l'interpréteur de commande de l'utilisateur.
"**grep root /etc/passwd | cut -d : -f7**"

18 -- Pour regarder la liste des utilisateurs de la machine j'ai utilisé
la commande ci-dessous.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image22.png)

Après quelques recherches sur internet, l'utilisateur « nobody »
correspond à un utilisateur à qui aucun fichier n'appartient, qui n'est
dans aucun groupe qui a des privilèges et dont les seules possibilités
sont celles que tous les « autres utilisateurs » (seulement le droit de
lire) ont. Il est courant de lancer des démons en tant que nobody pour 
des serveurs notamment de façon à limiter les dommages qui pourrait 
être occasionnés en cas d'attaques.

19 -- Par défaut, sudo conserve notre mot de passe en mémoire pendant 15
minutes. La commande qui permet de forcer sudo à oublier mon mot de
passe est "**sudo -k**"

**<ins>Exercice 2. Gestion des permissions</ins>**

1 -- J'ai premièrement créé un dossier nommé « test » grâce à la
commande « mkdir » puis ensuite j'ai créé un fichier grâce à la commande
« touch ». J'ai ensuite remplis ce fichier de quelques lignes de texte
avec la commande « nano fichier ». Les droits sur test et fichier sont
les suivants :

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image23.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image24.png)

2 -- J'ai d'abord retirez tous les droits sur « fichier » comme
ci-dessous.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image25.png)

Je suis ensuite passé en root pour modifier et afficher le fichier. La
modification du fichier a bien fonctionné malgré le fait que les droits
soient enlevés pour tout le monde. J'ai également pu l'afficher après
modification.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image26.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image27.png)

J'en conclus donc que l'utilisateur root à toutes les permissions même
si le fichier ne peut être ouvert par personne. Il peut donc tout faire
car il n'y a pas d'utilisateur plus haut que lui dans la hiérarchie.

3 -- J'ai commencé par donner à nouveau les droits en écriture et
exécutions à fichier.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image28.png)

Puis j'ai exécuté la commande demandée.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image29.png)

On peut dire que la commande précédente, qui remplace le contenu d'un
fichier s'il existe déjà à besoin des droits d'écriture sur le fichier
pour fonctionner. Les droits ne sont pas affectés par echo, echo 
remplace le "contenu" du fichier.

4 -- J'ai d'abord essayé d'exécuter le fichier normalement, puis avec
sudo, voici les résultats obtenus.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image30.png)

Cela ne fonctionne pas sans le sudo car nous n'avons pas les droits en
lecture. Cependant cela fonctionne avec sudo car on se met en mode
« super-utilisateur » et on surpasse ainsi les permissions.

5 -- J'ai retiré le droit de lecture pour ce répertoire.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image31.png)

On ne peut pas lister le contenu du répertoire, cependant on peut
exécuter et afficher le contenu du fichier fichier si on connais le
chemin complet.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image32.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image33.png)

J'en déduis donc que les droits du répertoire n'ont pas d'impacts sur
l'exécution des fichiers à l'intérieur de celui-ci, seulement s'il faut
faire des manipulations sur le répertoire en lui-même.

6 -- J'ai créé un nouveau fichier grâce à « mkdir » et un nouveau
fichier grâce à « touch ». J'ai retiré ensuite les droits en écriture au
fichier demandé avec la commande « chmod 555 nom_fichier ».

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image34.png)

Voici le résultat lorsque j'essaye d'écrire dans le fichier. Je n'ai pas
les permissions car je viens de m'enlever le droit en écriture dans ce
fichier.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image34.png)

Après avoir remis les droits d'écriture sur le dossier test, j'ai essayé
à nouveau d'écrire dans le fichier nouveau, mais je n'ai encore pas la
permissions.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image35.png)

J'ai ensuite supprimé ce fichjer, on m'a demandé si j'étais sûr de le
supprimer étant donné que le fichier est protégé en écriture.

Je peux donc déduire de toutes ces manipulations que les droits des
répertoires influent sur ceux des fichiers/répertoires à l'intérieur.
Le droit d’écriture sur un dossier ne donne pas le droit d’écrire dans les fichiers qu’il
contient. Il donne le droit de créer ou supprimer des fichiers dans ce dossier.

7 -- J'ai commencé par enlevé le droit en exécution du répertoire test.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image36.png)

J'ai donc essayé tout ce qui était demandé dans la question. Seul la
commande pour lister le contenu du répertoire à fonctionner.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image37.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image38.png)

J'en déduis donc que les droits du répertoire influent sur les
répertoires et fichiers se trouvant juste après. Le droit "**x**"
sur les dossiers donne l'autorisation d'accéder/traverser le dossier et
seulement la commande "**ls**" pour lister les dossier.

8 -- J'ai d'abord rétablie le droit en exécution du répertoire test.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image39.png)

Je me suis mis dans ce répertoire et j'ai à nouveau enlevé les droits
d'exécutions.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image40.png)

On ne peut toujours pas faire les commandes qui sont demandés, comme à
la question précédente car avoir les droits en lecture et écriture ne 
servent pas à grand chose si on n'a pas les droits en exécution.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image41.png)

J'en conclus que les droits du répertoire courant s'appliquent également
dans les répertoires qui se trouvent en-dessous dans l'arborescence.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image42.png)

On peut bien retourner dans le répertoire parent. Cela s'explique du
fait que sinon, on resterait bloqué dans ce répertoire.

9 -- J'ai rétablis les droits en exécution du répertoire test. Puis j'ai
attribué à fichier les droits suffisants pour qu'une autre personne de
mon groupe puis y accéder en lecture mais pas en écriture.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image43.png)

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image44.png)

Le deuxième chiffre ici concerne les utilisateurs de mon groupe donc 4
car il fallait ajouter seulement les droits en écriture. On peut utiliser 
aussi "**chmod g=r fichier**".

10 -- Le umask que j'ai choisis pour interdire à quiconque a part moi
l'accès en lecture ou en écriture ainsi que la traversée de mes
répertoires est 077.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image45.png)

11 -- Le umask que j'ai choisis pour autoriser tout le monde à lire vos
fichiers et traverser mes répertoires mais qui n'autorise que moi à
écrire est 022.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image46.png)

12 -- Le umask que j'ai choisis pour m'autoriser un accès complet et
autorise un accès en lecture aux membres de mon groupe est 027.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image47.png)

13 -- Voici les commandes en notations classiques passez en notation
octale :

-   chmod 534 fic

-   chmod 602 fic

-   chmod u-x, g+r, o+w fic

-   chmod 520 fic

14 -- Voici les droits sur le programme passwd que j'ai pu trouvé en me
rendant dans le répertoire /etc.

![](vertopal_ce31de2f17d04104a5c61947374a09f4/media/image48.png)

L'utilisateur à le droit de lire et de modifier le fichier ce qui est
normal dans le cas ou il aurait besoin de modifier son mot de passe. Les
groupes et les autres utilisateurs ne peuvent quand a eux que lire ce
fichier ce qui est normal car cela poserait d'énormes soucis si tout le
monde pouvait changer les mots de passes de tout le monde.
présence d’un indicateur particulier : ’s’ => setuid
un utilisateur lance ce programme en prenant l’identité de root => indispensable pour
qu’un utilisateur puisse modifier son mot de passe

