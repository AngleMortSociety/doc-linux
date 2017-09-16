
# Le système de fichier

Les dossiers ci-dessous sont majoritairement présents sur toutes les distributions GNU/Linux. Certaines différences existent néanmoins. Ce chapitre a été réalisé pour les distributions basées sur Debian.

## L'arborescence système

### /

Racine de l'arborescence. Il convient de noter qu'il n'existe pas de montage de disques comme sous Windows : `C:\` ou `D:\` n'existent pas.

### /bin

Abréviation de *binaries*, contient les fichiers binaires (exécutables) correspondant aux utilitaires de base du système.

### /boot

Tout petit répertoire contenant le noyau et les fichiers de ressources pour le chargeur d'amorçage (`grub`, par exemple).

`grub` est un programme qui s'occupe de lancer le système d'exploitation. Si vous installez plusieurs systèmes sur une machine, vous aurez, au démarrage, un menu et c'est grâce à `grub` que celui-ci s'affiche. Vous pouvez le configurer en changeant les paramètres dans `/boot/grub/menu.list`

### /dev

Abréviation de *devices*, contient les fichiers correspondant à tous les périphériques de votre machine.

### /etc

Abréviation de *Editable Text Configuration*, c'est le dossier le plus utilisé par l'administrateur puisqu'il contient tous les fichiers de configuration du système et de tous les logiciels installés. Ces derniers sont modifiables, d'où le nom du dossier même si les origines de celui-ci sont parfois contestées.

### /home

Contient le dossier personnel de chaque utilisateur (sauf *root* qui bénéficie d'un traitement à part, voir plus bas).

### /lib

Abréviation de *libraries*, contient toutes les bibliothèques de ressources et de fonctions nécessaires aux exécutables pour fonctionner (l'équivalent des DLL Windows), ainsi que les modules du noyau.

### /lost+found

Dossier dans lequel le système dépose des fichiers ou des morceaux récupérés en cas de crash ou de vérifications de fichiers.

### /media

Point de montage pour les médias amovibles tels que les disquettes ou CD-Rom, mais aussi les éventuels disques dur externes, clés USB, etc.

### /mnt

Abréviation de *mount*, point de montage pour les systèmes de fichiers temporaires ou réseau. A vous de choisir l'un ou l'autre de ces dossiers (`/media` ou celui-ci) pour monter vos périphériques. Cela n'a pas d'incidence sur le système.

### /opt

Abréviation de *optional*, contient les paquets logiciels complémentaires au système que vous installez en supplément. Certaines distributions, comme Debian ou Ubuntu, l'utilisent très peu mais il reste néanmoins présent.

### /proc

Abréviation de *processus*, le noyau place dans ce répertoire virtuel (il n'existe qu'en mémoire et pas vraiment sur le disque) toutes les données concernant les processus en cours d'exécution.

### /root

Dossier personnel du « **super user** » (*super-utilisateur*, en français).

### /run

Géré par le système, concerne les fichiers temporaires ou les fichiers d'exécution.

### /sbin

Abréviation de *system binaries*, contient les exécutables pour les administrateurs du système (applications de plus bas niveau).

### /selinux

Abréviation de *secure Linux*, permet de définir une politique de contrôle d'accès obligatoire aux éléments du système.

### /srv

Abréviation de *services*, contient les données hébergées par le système, certaines distributions ne l'utilisent pas (Debian et dérivés préfèrent le dossier `/var`). Anciennement utilisé pour stocker des données par des applications ou fonctionnalités serveur à destination de l'administrateur.

### /sys

Abréviation de *system*, parfois utilisé par le noyau pour échanger des données avec d'autres applications fonctionnant dans le « user space » (*espace utilisateur*, en français).

### /tmp

Abréviation de *temporary*, contient tous les fichiers temporaires que le système est amené à créer. Vous pouvez l'utiliser mais attention, ce dossier est vidé à chaque démarrage, de plus il possède le « sticky bit ».

### /usr

Abréviation de *Unix System Ressources*, contient certains dossiers semblables à ceux présents à la racine mais qui ne sont pas nécessaires au fonctionnement minimal du système. Certains utilisateurs utilisent ces sous-dossiers pour ne pas modifier la structure originale du système.

#### /usr/bin

Binaires exécutables, en complément de `/bin`, contient tous les binaires installés sur votre machine par les utilisateurs avec le gestionnaire de paquets RPM.

#### /usr/lib

Bibliothèques partagées.

#### /usr/local

Fichiers locaux à la machine ou à son architecture (à ne pas partager sur un réseau, par exemple).

#### /usr/sbin

Binaires pour l'administrateur, en complément de `/sbin`

#### /usr/share

Fichiers indépendants de la plateforme (non binaires).

#### /usr/src

Sources des applications.

#### /usr/X11R6

Fichiers concernant l'interface graphique. X11 ou *X Window System* sont des environnements graphiques de type « fenêtré ».

### /var

Abréviation de *variables*, dossier contenant les fichiers régulièrement modifiés (comme les journaux système, les bases de données ou les boîtes aux lettres).

#### /var/lock

Fichiers de verrouillage, permet de connaître quelles ressources sont en cours d'utilisation.

#### /var/log

Contient les fichiers de journalisation (fichiers de log).

#### /var/mail

Boîtes aux lettres des utilisateurs.

#### /var/spool

Files d'attente des services.

#### /var/www

Contient vos applications web et pages HTML hébergés par votre serveur. Si ce dossier n'existe pas, c'est certainement qu'aucun serveur n'est installé sur votre système.

## Les fichiers de configurations

### /etc/profile

Configurations concernant tous les utilisateurs, quel que soit le *shell* de connexion.

### /etc/bash.bashrc

Configurations du *shell* `bash` pour tous les utilisateurs.

### /home/user/.profile

Configuration personnalisé de l'utilisateur, quel que soit le *shell* utilisé (ce fichier est prioritaire sur `/etc/profile`).

### /home/user/.bashrc

Configuration personnalisé de l'utilisateur pour le *shell* `bash` (ce fichier est prioritaire sur `/etc/bash.bashrc`).

Note : Après modification d'un fichier `profile` ou `bashrc`, il faudra prendre en compte les nouvelles modifications. Vous avez deux solutions :

1. Quitter le Terminal ou votre connexion SSH et vous reconnecter.
2. Utiliser la commande `source` (`source .profile` ou `source .bashrc`).

### /etc/passwd

Liste de tous les utilisateurs du système (avec leur configuration).

### /etc/group

Liste de tous les groupes du système.

### /etc/shadow

Liste des mots de passes chiffrés.

### /etc/sudoers

Fichier qui détermine quels utilisateurs ont la possibilité d'utiliser la commande `sudo`. Pour modifier ce fichier, utilisez la commande :

``` bash
sudo visudo
```
