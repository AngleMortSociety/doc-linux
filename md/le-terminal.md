
# Le Terminal

## Connexion

Le Terminal devient rapidement incontournable dès que l'on souhaite utiliser pleinement un système GNU/Linux. Que vous souhaitiez vous connecter à un serveur distant, utiliser une distribution sans gestionnaire de bureau (*Gnome*, *KDE*, *Xfce*, etc.), utiliser le mode "rescue" ou encore intervenir sur une machine qui connait un problème avec la carte graphique, le Terminal permet d'exécuter des commandes et de réaliser toute tâche que vous feriez autrement via une interface graphique. Plus rustique, le Terminal est bien plus puissant et parfois même plus rapide qu'un gestionnaire de bureau. Il permet de lancer des scripts qui peuvent être horodatés par l'intermédiaire d'une crontab, d'exécuter des commandes pour la maintenance du système, de télécharger des fichiers, de gérer des services, de réaliser une sauvegarde de vos fichiers et bien plus encore.

Pour les distributions GNU/Linux avec un gestionnaire de bureau, il est possible d'ouvrir un Terminal en mode plein écran. Pour ce faire, choisissez la combinaison de touches suivante : <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>F1</kbd> (ou avec <kbd>F2</kbd>, <kbd>F3</kbd>, <kbd>F4</kbd>, <kbd>F5</kbd> ou <kbd>F6</kbd> pour choisir le Terminal). Pour en sortir, utilisez la combinaison de touches <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>F7</kbd> (attention toutefois, il sera parfois nécessaire de tâtonner en essayant les touches <kbd>F5</kbd>, <kbd>F6</kbd>, <kbd>F8</kbd>, <kbd>Fx</kbd>... Tout dépend de la distribution installée car ceci n'est pas une règle absolue).

Pour ouvrir une console sous le bureau Gnome, allez dans le menu Applications ➞ Accessoires ➞ Terminal. La touche de raccourci pour ouvrir une fenêtre de Terminal est <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>T</kbd> ou <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>T</kbd>.

Pour savoir sur quel Terminal vous êtes connecté, regardez la barre de titre qui indique son numéro. Si celui-ci n’est pas indiqué, vous pouvez entrer la commande `tty` pour l’obtenir.

Si vous voulez savoir quels sont les *shell* installés sur votre système, utilisez la commande suivante :

``` bash
more /etc/shells
```

Pour connaître le *shell* en cours d'utilisation, entrez :

``` bash
echo $SHELL
```

Ou bien :

``` bash
printenv SHELL
```

Ou encore :

``` bash
ps
```

### Mac OS X

Sous Mac OS X, le Terminal se trouve dans le dossier `/Applications/Utilities/`. À partir de *Lion* (version 10.7), vous le trouverez aussi dans le *Launchpad* (dossier *outils* ou *autre*) ou encore avec une recherche *Spotlight* que vous pouvez appeler avec le raccourci suivant : <kbd>CMD</kbd> + <kbd>ESPACE</kbd>.

### Windows

Sur bien des aspects, Windows est très différent par rapport aux distributions GNU/Linux.

Pour simuler un environnement [UNIX][], il vous faudra utiliser le logiciel [Cygwin][], plus d'informations sur [Wikipedia][]. Après installation de celui-ci, vous aurez alors accès à un Terminal. Attention toutefois, toutes les commandes ne vous seront pas accessibles et vous ne pourrez pas installer de nouveaux programmes via un gestionnaire de paquets.

## Fonctionnement

L’invite de commande (appelée couramment le *shell* ou *bash*) est représentée généralement comme ceci (il est possible de le configurer) : `login@login-desktop:~$`.

Le *login* indique le nom de l'utilisateur et *login-desktop*, le nom de la machine où vous êtes connecté. Le tilde « ~ » représente le dossier *home* de l'utilisateur. Le « $ » est le compte utilisateur normal alors que le dièse « # » est réservé pour le compte *admin* (ou *root*).

Le Terminal est sensible à la casse, c'est à dire qu'il distingue les majuscules des minuscules. Ainsi la commande `ls` fonctionnera alors que `LS` ou encore `Ls` afficheront des erreurs.

Une différence notable par rapport à Windows est le symbole destiné à séparer les dossiers. Pour le système de Microsoft, c'est l'anti-slash « \ » qui est utilisé mais sous Linux il s'agît du slash « / ». Exemple : `/home/user/documents`.

Concernant la représentation des dossiers, il faut connaitre les différentes significations :

- « . »		: est le dossier courant, celui où se trouve actuellement l'utilisateur
- « .. »	: représente le dossier parent
- « ~ »		: le *tilde* représente le dossier utilisateur (dossier *home*)

Il est possible d'utiliser des fichiers ou des dossiers cachés au sein du système. Dans ce cas, le nom commence systématiquement par un point « . ».

Quand vous interrogez le système par l'intermédiaire d'une commande pour avoir des informations sur certains fichiers, il est possible d'utiliser des jokers. Ceux-ci permettent de trouver, en une seule instruction, une série de fichiers. Si un nom précis vous échappe, ils peuvent ainsi vous aider à retrouver les fichiers oubliés. Par exemple, si vous souhaitez lister tous les fichiers au format *jpg* de votre dossier image, vous pouvez entrer ceci :

``` bash
ls *.jpg
```

Cela a pour effet de lister tous les fichiers (quels que soient leurs noms) possédant l'extension *.jpg*.

L'étoile « * » représente un nombre indéfini de caractères quelconques alors que le point d'interrogation « ? » représente un caractère unique. Il est aussi possible d'utiliser des crochets « [] » :

- « [a] »	: signifie égal à "a" (`ls *[a]*` liste tous les fichiers contenant la lettre "a")
- « [!a] »	: signifie différent de "a" (`ls *[!a]*` liste tous les fichiers, sauf ceux contenant la lettre "a")
- « [abc] »	: signifie que l'un des caractères est "a", "b" ou "c" (`ls [abc]*` liste tous les fichiers commençant par "a", "b" ou "c").
- « [a-l] »	: signifie que le caractère est compris entre "a" et "l" (`ls img[a-l]*` liste tous les fichiers commençant par *img* suivi d'une quelconque lettre entre "a" et "l").

### Notes

Certaines commandes, comme `apt-get` ou `aptitude` peuvent vous demander une confirmation, généralement notée `[YES/no]`, `[Y/n]` ou `[yes/NO]`, `[y/N]`. La validation avec la touche <kbd>ENTRÉE</kbd> valide le choix en majuscule.

Quand il est nécessaire d'entrer un mot de passe, aucun caractère n'est affiché lors de votre saisie. Ceci est parfaitement normal, il ne s'agît que de sécurité. En effet, il est plus difficile de connaître le nombre de caractères utilisés pour un intrus regardant votre écran.

## Écrire une commande

Dans un Terminal, il suffit d'écrire le nom de la commande souhaitée pour interagir avec le système :

``` bash
commande
```

Par exemple, pour lister les fichiers d'un dossier, il faudra utiliser la commande suivante :

``` bash
ls
```

Mais, toutes les commandes GNU/Linux (à quelques exceptions près), acceptent des options. Celles-ci permettent de modifier le résultat en fonction de vos attentes.

``` bash
commande -option(s)
```

Toujours avec ls, le résultat pourrait ressembler à ceci :

``` bash
ls -a
```

Il est possible d'avoir plusieurs paramètres :

``` bash
ls -a -l
```

Mais il est tout à fait possible de les réunir pour avoir une ligne de commande plus courte, comme ici :

``` bash
ls -al
```

La plupart des options *courtes* possèdent des versions dites *longues* mais il existe aussi des options uniquement de type *longue*, par exemple :

``` bash
tty --help
```

Notez les deux tirets qui permettent de faire la différence entre les options *courtes*...

``` bash
ls -a
```

... et les options *longues* :

``` bash
ls --all
```

Enfin, quand une option a besoin d'une valeur, il est nécessaire de l'indiquer directement à sa suite :

``` bash
commande -option valeur
```

Pour les options longues, il est nécessaire d'avoir un signe égal et aucun espace :

``` bash
commande --optionLongue=valeur
```

## Chemin relatif et absolu

Prenons comme référence cette arborescence : `/home/user/musique/albums/groupe/`. La différence entre les deux types de chemin peut s'expliquer de la façon suivante :
- Le chemin relatif commence à votre position actuelle. Si vous êtes dans votre dossier `home` et que vous souhaitez atteindre un morceau de musique, vous pouvez écrire `cd musique/albums/groupe/`
- Le chemin absolu, lui, commence toujours par la racine. Quelle que soit votre position actuelle, vous pouvez donc atteindre l’endroit désiré par : `cd /home/user/musique/albums/groupe/`

## Tout est fichier

Sous Linux, il y a une règle d'or : **tout est fichier**. Un disque dur, une clé USB, un dossier, un utilisateur ou encore le clavier sont représentés dans le système comme des fichiers. De plus, il n'y a pas de hiérarchie dans le fonctionnement des droits : un fichier a un seul propriétaire. Concernant le groupe, c’est la même chose : un fichier n'appartient qu'à un seul et unique groupe. Les autres utilisateurs de la machine constituent le « reste du monde » (*other*). Il faut éviter, dans certains systèmes, d'avoir un nom de dossier `home` identique à un nom d'utilisateur car cela peut créer des problèmes, surtout pour les systèmes embarqués. De plus, tout fichier commençant par un point est un fichier « caché ». Nous reviendrons sur ces principes dans les chapitres suivants.

## S'orienter dans le Terminal

Vous pouvez utiliser les flèches ( <kbd>↑</kbd> et <kbd>↓</kbd> ) de votre clavier afin de visualiser les commandes précédemment utilisées.

Lorsque vous tapez les premières lettres d'une commande (ou d'un fichier présent dans le dossier), vous pouvez appuyer sur la touche <kbd>TAB</kbd>, l'auto-complétion devrait faire le reste. Si vous entendez un bip sonore, appuyez une seconde fois sur cette touche pour avoir une liste des choix possibles. Pour avoir la liste complète de toutes les commandes disponibles sur votre système, appuyez deux fois de suite sur <kbd>TAB</kbd>, en ayant au préalable vérifié que le prompt (la ligne de commande) est vide, et confirmer l'action.

### L'historique

La commande `history` affiche la liste de toutes les commandes exécutées dans le Terminal. Pour plus d'informations sur celle-ci, reportez-vous au chapitre sur les commandes. Dans le dossier `home` de chaque utilisateur se trouve le fichier *.bash_history* qui contient l'historique complet.

### Trouver une commande

Pour savoir où se trouve une commande dans votre système ou tout simplement pour savoir si elle existe, entrez :

``` bash
which commande
```

### Retrouver le nom d'une commande

Il arrive de savoir globalement ce que l'on cherche, mais de ne pas avoir le nom précis d'une commande. Pour cela, écrivez :

``` bash
apropos mot-clé mot-clé mot-clé
```

Accessoirement, il est possible d'avoir une brève description de la commande (description que l'on retrouve avec la commande `whatis`) :

``` bash
apropos commande
```

### Trouver de l'aide dans le Terminal

L’invite de commande étant plus épurée qu'une interface graphique, il est nécessaire d'avoir les bons outils pour trouver de l'aide.

#### Le Man

Abréviation de *manual* (ou *manuel*, en français). Si vous devez connaître une seule commande sous GNU/Linux, c'est celle-ci. Elle permet d'afficher l'aide d'une commande et de comprendre comment elle fonctionne (touche <kbd>q</kbd> pour revenir au Terminal) :

``` bash
man commande
```

#### Help

De nombreuses commandes possèdent l'option `-h` ou `--help` qui donne en général un minimum d'informations. Celles-ci sont parfois très synthétiques, parfois très complètes.

``` bash
commande -h
```

#### info

Alternative de la commande `man`, elle permet de lire les documentations au format *info*. Appuyez sur la touche <kbd>q</kbd> pour revenir au Terminal.

``` bash
info commande
```

#### Konqueror

Il est possible sous Konqueror, mais aussi avec certains autres navigateurs, d'entrer dans la barre d'adresse `info:bash` ou `man:bash` pour consulter les pages correspondantes plus confortablement.

#### OS X

Dans le même ordre d'idée, pour lire le manuel de façon plus agréable sous OS X, il suffit d'écrire (exemple avec la commande `top`) :

``` bash
man -t top | open -fga Preview
```

### Gagner du temps

Pour récupérer la dernière ligne de commande dans un Terminal, il faut utiliser deux points d'exclamation « !! ». Par exemple, on peut exécuter une commande :

``` bash
commande-1
```

Et, ensuite, on peut exécuter une autre commande en récupérant la dernière précédemment exécutée :

``` bash
commande-2 !!
```

Enfin, si l'on souhaite juste reproduire la dernière commande entrée :

``` bash
!!
```

Dans le même ordre d'idée, il est possible de récupérer les arguments de la dernière commande exécutée au sein du Terminal avec un point d'exclamation suivi d'une étoile « !* » :

``` bash
commande-1 argument
```

Et pour la suivante :

``` bash
commande-2 !*
```

Un exemple concret :

``` bash
mkdir test
cd !*
```

Il est également possible d'utiliser la variable d'environnement `$_` pour appeler le dernier argument utilisé.

### Nettoyer l'écran

A force de manipulations, il est probable que le Terminal s’encombre et qu’il devienne peu lisible. Pour y voir plus clair, utilisez la commande `clear` ou le raccourci clavier <kbd>CTRL</kbd> + <kbd>L</kbd>.

### Les touches de raccourcis

Dans un Terminal, il est possible d'utiliser les raccourcis suivants :

| Raccourci														| Détail 																														|
| :------------------------------------------------------------	| :----------------------------------------------------------------------------------------------------------------------------	|
| Les flèches <kbd>↑</kbd> et <kbd>↓</kbd>						| Navigation de l'historique pour les commandes précédemment utilisées.															|
| <kbd>SHIFT</kbd> + ( <kbd>↑</kbd> ou <kbd>↓</kbd> )			| Permet de scroller le contenu du Terminal (la molette de la souris est tout aussi efficace).									|
| <kbd>SHIFT</kbd> + ( <kbd>Page up</kbd> ou <kbd>down</kbd> )	| Même chose mais de page en page.																								|
| <kbd>CTRL</kbd> + <kbd>C</kbd>								| Arrête un processus en cours de fonctionnement.																				|
| <kbd>CTRL</kbd> + <kbd>D</kbd>								| Ferme le terminal en cours d'utilisation ou quitte un utilisateur substitué (similaire aux commandes `exit` et `logout`).		|
| <kbd>CTRL</kbd> + <kbd>L</kbd>								| Permet de nettoyer le Terminal, le curseur remonte en haut (similaire à la commandes `clear`).								|
| <kbd>CTRL</kbd> + <kbd>Z</kbd>								| Stoppe le processus en cours, mais ne le détruit pas : il reste en attente. Tapez `fg` pour le faire revenir au premier plan.	|
| <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>DEL</kbd>				| Diffère en fonction des distributions GNU/Linux.																				|

Il est à noter que ces raccourcis peuvent avoir différents résultats en fonction des systèmes GNU/Linux utilisés.

## Les droits

Quand vous listez le contenu de votre disque dur avec la commande `ls -lh` vous obtenez quelque chose comme (exemple sur un fichier) :

``` bash
-rw-r--r-- 1 martin staff 1,9M 4 sep 19:42 photo.jpg
```

### Décomposition des informations

Le tout premier caractère de cet exemple indique le type de fichier : ici, c’est un simple fichier. D’autres caractères peuvent représenter les différents types ; en voici la liste exhaustive :

| Option 		| Signification	| Détail 																				|
| :------------	| :------------	| :------------------------------------------------------------------------------------	|
| *-*			| *nothing*		| N’indique rien de particulier, c'est un fichier classique.							|
| *d*			| *directory*	| Indique que c'est un dossier.															|
| *l*			| *link*		| Indique que c'est un lien symbolique (les liens physiques ne sont pas représentés).	|
| *c*			| *char*		| Indique que c'est un périphérique de type caractère.									|
| *b*			| *block*		| Indique que c'est un périphérique de type bloc.										|
| *p*			| *pipe*		| Indique que c'est un pipe.															|
| *s*			| *socket*		| Indique que c'est un socket.															|

Ensuite, le premier groupe de caractères `rw-`, correspond au propriétaire du fichier. Le second `r--` représente le groupe et le dernier `r--` représente les autres utilisateurs. On appelle parfois `r`, `w` et `x` des « flags » ou « drapeaux ». La signification des lettres est la suivante :

| Droit 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-*			| *nothing*		| Aucun droit de lecture, d'écriture ou d'exécution possible.		|
| *r*			| *read*		| Droit de lecture : vous pouvez examiner le fichier.				|
| *w*			| *write*		| Droit d'écriture : vous pouvez apporter des modifications.		|
| *x*			| *execute*		| Droit d'exécution : valable pour un script ou un binaire.			|

Note : le `x` est spécifique dans le cas d'un dossier car il donne le droit d'accéder ou non au contenu de celui-ci.

Pour résumer, le premier caractère symbolise le type (fichier, dossier ou lien symbolique, etc.). Vient ensuite le premier groupe de 3 qui représente les droits du propriétaire sur ce fichier, puis les droits du groupe et enfin, les droits des autres utilisateurs. L'ordre reste immuable : `r`, `w` et, pour finir la gamme, `x`. En cas de non-droit, le symbole `-` est alors utilisé.

Puis vient le nombre 1 qui représente le fichier, c'est-à-dire qu'il y a un fichier unique. Si des liens physiques sont créés, alors ce nombre augmentera autant de fois qu'il y aura de liens pointant vers celui-ci. Les liens symboliques ne sont pas comptabilisés.

Ensuite, c’est le nom de l'utilisateur. Dans l'exemple, il s'agit de *martin*. Le nom suivant, ici *staff*, est le nom du groupe. On sait donc que *martin* a des droits de lecture et d'écriture en tant que propriétaire de son fichier alors que le groupe *staff* n'a des accès qu'en lecture tout comme les autres (le reste des utilisateurs qui ne font pas partie de ce groupe).

Si vous avez deux utilisateurs dans le même groupe mais que vous ne voulez pas qu'ils aient les mêmes droits (de groupe) sur ce fichier, alors vous avez deux solutions :

- Soit, vous retirez un des utilisateurs du groupe.
- Soit, vous utilisez les paramètres étendus (ACL).

Les autres informations du fichier indiquent, dans l'ordre, le poids du fichier *1,9 M* (grâce à l'option *h*), la date *4 sep*, l'heure de la dernière modification *19:42* et enfin, le nom du fichier *photo.jpg*.

## Droits étendus

Pour rendre possible une gestion plus poussée des permissions, il existe d'autres droits spéciaux.

### Droit SUID

Ce droit s'applique aux fichiers exécutables. Il permet d'allouer temporairement à un utilisateur les droits du propriétaire du fichier durant son exécution. En effet, lorsqu'un utilisateur exécute un programme, les tâches accomplies par ce dernier sont restreintes par les droits de cet utilisateur. Lorsque le droit SUID est appliqué à un exécutable et qu'un utilisateur quelconque l'exécute, le programme détient alors les droits du propriétaire du fichier durant son exécution. Bien sûr, un utilisateur ne peut jouir du droit SUID que s'il ne détient par ailleurs les droits d'exécution du programme. Ce droit est utilisé lorsqu'une tâche, bien que légitime pour un utilisateur classique, nécessite des droits supplémentaires (généralement ceux de *root*). Il est donc à utiliser avec précaution. Pour des partitions supplémentaires, il faut activer le bit `suid` pour pouvoir l'utiliser en le spécifiant dans les options des partitions concernées dans le fichier `fstab`.

Son flag est la lettre `s` ou `S` qui vient remplacer le `x` du propriétaire. La majuscule sur le flag permet de voir le flag `x` (droit d'exécution du propriétaire) caché par le droit SUID. C'est un `s` si le droit d'exécution du propriétaire est présent et un `S` dans le cas inverse.

Le droit SUID possède la valeur octale 4000. Un fichier avec les droits suivants (755) correspondant à : `-rwxr-xr-x`, serait représenté sous cette forme (4755) : `-rwsr-xr-x`.

### Droit SGID

Pour les fichiers, ce droit fonctionne comme celui du SUID mais appliqué aux groupes. Il donne à un utilisateur les droits du groupe auquel appartient le propriétaire de l'exécutable et non plus les droits du propriétaire.

Concernant les dossiers, ce droit a une tout autre utilisation. Normalement, lorsqu'un fichier est créé par un utilisateur, ce dernier en est propriétaire et un groupe par défaut lui est appliqué. Cependant, lorsqu'un fichier est créé dans un répertoire portant le droit SGID, alors ce fichier se voit attribuer par défaut le groupe du répertoire. De plus, si c'est un autre répertoire qui est créé dans le répertoire portant le droit SGID, ce sous-répertoire portera également ce droit.

Le droit SGID possède la valeur octale 2000. Un fichier avec les droits suivants (755) correspondant à : `-rwxr-xr-x`, serait représenté sous cette forme (2755) : `-rwxr-sr-x`.

### Le sticky bit

Lorsque ce droit est positionné sur un répertoire, il interdit la suppression d'un fichier à tout utilisateur autre que le propriétaire. Néanmoins, il est toujours possible pour un utilisateur possédant les droits d'écriture sur ce fichier de le modifier. La création de nouveaux fichiers est toujours possible pour tous les utilisateurs possédant le droit d'écriture sur ce répertoire.

Pour les fichiers, l'utilisation est tout autre. En effet, le droit indique alors que ce fichier doit encore rester en mémoire vive après son exécution. Le but était, autrefois, d'améliorer les performances en évitant de charger/décharger un fichier de la mémoire (par exemple, un exécutable ou une bibliothèque logicielle). Le terme « sticky » (collant) voulait dire que le fichier restait collé en mémoire. Cette pratique est désormais obsolète.

Le droit « sticky bit » possède la valeur octale 1000. Un dossier avec les droits suivants (755) correspondant à : `drwxr-xr-x`, serait représenté sous cette forme (1755) : `drwxr-xr-t`.

### ACL

Avec le système de permissions GNU/Linux, il n'est pas possible d'avoir une gestion très fine des droits. Il est seulement possible de donner des droits particuliers à :

- 1 utilisateur (*user*),
- 1 groupe d'utilisateurs (*group*),
- ceux qui ne sont ni l'un, ni l'autre (*other*).

Cependant, cette méthode ne couvre pas suffisamment de cas, notamment en entreprise. En effet, les réseaux d'entreprises nécessitent l'attribut de droits pour certains membres de plusieurs groupes distincts. Les ACL, Access Control List (ou *liste de contrôle d'accès*, en français) répondent à ce besoin. Il existe deux prérequis :

- Que le noyau supporte les ACL.
- Que le système de fichier soit monté avec l'option `acl`.

Sur certaines distributions GNU/Linux, il est nécessaire d'installer le paquet correspondant (`acl` dans les archives *debian*). Un fichier disposant d'une liste d'ACLs est représenté avec un `+` en fin de ligne : `-rwxr-xr-x+`

## Le PID

Le PID, pour Process IDentifier (*identifiant de processus*), est un code unique attribué à tous les processus et toutes les commandes lors de leurs premières exécutions. Il disparait lors de la fermeture du processus ou à la fin de l'exécution de la commande afin d'être réattribué. Le PID permet ainsi d'identifier ces dernières avec la plupart des commandes qui s'appliquent sur un processus donné (comme la commande `kill`). Sous une distribution GNU/Linux, le premier programme démarré, `init`, prend le PID 1. Les processus suivants incrémentent ce numéro pour arriver à 32768 par défaut (réglable avec le fichier `/proc/sys/kernel/pid_max`) pour repartir de 2 en évitant les PID déjà attribués.

L'identifiant de processus parent ou PPID, pour Parent Process IDentifier d'un processus est, dans les systèmes GNU/Linux, le PID du processus ayant initié sa création (via l'appel système `fork`).

## Flux et redirections

L'environnement GNU/Linux confère à chaque application exécutée, les flux d'entré et de sortie (*stdin*, *stdout*, *stderr*), en plus des flux stockés (*fichiers*) ou en transit (exemple : *tube nommé*). Chaque processus possède donc trois descripteurs de flux :

- l'*entrée standard*, qui permet d'envoyer des données au programme
- la *sortie standard*, qui est utilisée pour afficher les résultats d'un programme
- la *sortie standard des erreurs*, qui permet d'afficher les messages correspondants aux erreurs survenues lors de l'exécution du programme.

Par défaut, les deux flux de sortie sont envoyés sur le Terminal de l'utilisateur (l'écran) et l'entrée prend ses données depuis le clavier. Comme avec les fichiers standards, il est possible de lire (sortie) et d'écrire (entrée) sur les descripteurs de flux.

### Les chevrons

Si vous souhaitez rediriger le résultat de votre commande dans un fichier, les chevrons sont alors nécessaires. Par exemple, si vous faites un `ls -a`, le résultat vous sera affiché à l'écran. Maintenant avec un `ls -a > fichier.txt` le résultat ne sera pas affiché mais écrit dans un fichier au nom de *fichier.txt*. Si le fichier existe, il sera écrasé, sinon il sera tout simplement créé à l'exécution de la commande.

Avec un `ls -a >> fichier.txt`, le fichier sera créé si il n'est pas déjà présent sur le disque. Dans le cas contraire, le résultat de cette commande sera ajouté à la fin du fichier. Pour ne pas garder le résultat d'une commande et ne pas l'afficher sur l'écran, redirigez la sortie sur : `/dev/null`.

Pour rediriger uniquement les erreurs, utilisez `ls -a 2> erreur.log` ou `ls -a 2>> erreur.log`.

Pour utiliser des entrées d'un fichier ou du clavier, il faut utiliser des chevrons inverses. On peut utiliser la commande `cat` pour créer un fichier rapidement : `cat <<FIN > fichier`. Le mot clé « FIN » est choisi par vos soins et il détermine la fin de la saisie (attention à la casse).

#### En résumé

- `>` ou `1>` redirige la sortie dans un fichier (s'il existe déjà, il sera écrasé).
- `>>` ou `1>>` redirige la sortie à la fin d'un fichier (s'il n'existe pas, il sera créé).
- `2>` redirige les erreurs dans un fichier (s'il existe déjà, il sera écrasé).
- `2>>` redirige les erreurs à la fin d'un fichier (s'il n'existe pas, il sera créé).
- `2>&1` redirige les erreurs au même endroit et de la même façon que la sortie standard.

### Le tube

Ou « pipe », permet de rediriger la sortie standard d'une commande vers l'entrée standard d'une autre commande. Pour afficher le résultat de `ls` en mode de lecture avec `less`, il faut écrire :

``` bash
ls -FlAh | less
```

Il permet aussi de connecter la sortie d'erreur de la commande-1 sur l'entrée de la commande-2 :

``` bash
commande-1 |& command-2
```

### L'esperluette

Elle désigne le logogramme « & » (esperluette ou esperluète ou encore « ET » commercial). Elle peut être utilisée à diverses fins. La première ne permet l'exécution d'une commande que si la précédente s'est déroulée sans incident :

``` bash
aptitude update && aptitude -y upgrade
```

L'inverse est d'utiliser deux tubes « &#124;&#124; » ; la deuxième commande ne sera exécutée que si la première se termine avec une erreur :

``` bash
commande-1 || commande-2
```

Une utilisation différente en est faite en la plaçant à la suite d'une commande. Ceci a pour effet de lancer cette dernière en tâche de fond. Reportez-vous au chapitre « Commandes en tâche de fond » pour plus de détails :

``` bash
commande-1 &
```

Il est possible de lancer plusieurs commandes de cette façon sur une ligne :

``` bash
commande-1 & commande-2 & commande-3
```

Cela lance les différentes commandes de manière asynchrone. Les valeurs numériques affichées entre crochets, une fois les exécutions terminées, correspondent aux numéros des tâches suivis des identifiants de processus de chacune des commandes ainsi exécutées. Il est à noter, dans l'exemple précédent, que la `commande-3` n'est pas lancée en tâche de fond car aucune esperluette ne la succède.

### Lancer plusieurs programmes

Une autre solution pour exécuter des commandes les unes après les autres est d'utiliser le point-virgule « ; », comme ceci :

``` bash
commande-1 ; commande-2 ; commande-3
```

Notez-bien qu'elles sont toutes indépendantes les unes des autres.

## Commandes en tâche de fond

Il existe deux façons d'avoir des commandes en tâche de fond :

1. Comme vu précédemment, avec une esperluète « & », qui fait suite à une commande
2. Avec la combinaison de touche <kbd>CTRL</kbd> + <kbd>Z</kbd> qui a pour effet de stopper le processus et de le mettre en attente

Dans le chapitre qui est consacré à la commande `screen`, nous verrons une troisième possibilité.

On place une commande en arrière-plan quand son exécution prend du temps et que l'on veut garder la main pour effectuer d'autres tâches (le système est multitâche). Il existe trois commandes primaires pour contrôler les commandes en tâches de fond :

- `jobs`	: affiche l'état des tâches
- `fg`		: déplace une tâche au premier plan
- `bg`		: déplace une tâche en arrière-plan comme si elle avait était lancée avec « & »

La commande `jobs` n'affiche rien quand la liste des tâches de fond est vide. Dans le cas contraire, vous aurez quelque chose comme ceci :

``` bash
[1]+ En cours d'exécution	top &
[2]+ Stoppé	sleep 2m &
[3]+ En cours d'exécution	autreCommande &
etc.
```

Pour interagir avec l'une des tâches listées ci-dessus, il faut utiliser le symbole pourcentage « % » suivi du numéro qui désigne la commande choisie. Dans l'exemple précédent, la première commande « En cours d'exécution » est active. Pour reprendre la main sur celle-ci et la faire passer au premier plan de votre Terminal, utilisez la commande `fg`, comme ceci :

``` bash
fg %1
```

Quand une commande est active dans le Terminal (`sleep`, par exemple), la combinaison de touches <kbd>CTRL</kbd> + <kbd>Z</kbd> passe cette commande en arrière-plan mais en mode « Stoppé ». Pour la relancer, afin qu'elle continue de s'exécuter en arrière-plan, utilisez la commande `bg`, comme ceci :

``` bash
bg %2
```

En utilisant la commande `jobs`, certaines commandes peuvent afficher le mot-clé « Fini » afin de vous avertir que la tâche s'est terminée. Si vous faites de nouveaux appel à `jobs`, la commande ne sera pas listée une seconde fois.

La commande `kill` utilise le PID pour arrêter une commande en cours d'exécution. Dans le cas d'une tâche, il est alors possible d'utiliser cette commande de la même manière que précédemment avec les commandes `fg` et `bg`, c'est à dire en utilisant le symbole pourcentage « % » suivi d'un numéro qui représente la commande choisie :

``` bash
kill %3
```

Dans ce cas, la commande sera indiquée comme « Complétée » et se terminera.

## Configuration

### Fichiers bashrc et profile

Comme vu dans le chapitre « Le système de fichier », plusieurs éléments peuvent être configurés dans ces fichiers. En fonction du fichier modifié, il affectera tous les utilisateurs (`/etc/profile` ou `/etc/bash.bashrc`) ou uniquement l'utilisateur courant (`/home/user/.profile` ou `/home/user/.bashrc`). Des alias peuvent être définis dans ces fichiers, des scripts peuvent être exécutés lors de la connexion d'un utilisateur, etc.

En fonction des distributions installées sur votre système, ces fichiers seront plus ou moins configurés. Souvent, certaines parties sont désactivées et commentées, libre à vous d'enlever les dièses « # » pour les rendres actives et éventuellement les modifier en fonction de vos besoins.

### Éditeur de texte par défaut

Généralement, l'éditeur de texte par défaut d'une distribution GNU/Linux est `nano`. Il convient à la plupart des utilisations mais il se peut que vous en souhaitiez un autre. Pour cela :

``` bash
sudo select-editor
```

Il est possible que cette commande ne soit pas disponible en fonction des distributions GNU/Linux. Dans ce cas, essayez ceci :

``` bash
sudo update-alternatives --config editor
```

Il ne reste plus qu'à choisir le numéro en fonction des éditeurs affichés dans le tableau et d'appuyer sur la touche <kbd>ENTRÉE</kbd>.

### Invite de commande

Pour personnaliser l'invite de commande du Terminal, il est nécessaire de modifier les variables `$PS1` et éventuellement `$PS2`. Il existe aussi les variables `$PS3` et `$PS4`. Voici le champ d'action de chacune de ces variables :

1. `$PS1` : représente la chaîne principale de l’invite de commande.
2. `$PS2` : invite secondaire affichée lorsque le `bash` a besoin d’informations supplémentaires (par défaut `>`).
3. `$PS3` : chaîne de l’invite de la commande `select` (par défaut `#?`).
4. `$PS4` : chaîne de l’invite de l’option *xtrace* (par défaut `+`).

Puisque l’invite n’est utile que si `bash` est employé en mode interactif, il est préférable de la définir globalement dans `/etc/bashrc` ou localement dans `~/.bashrc`.

Voici un exemple de configuration :

``` bash
export PS1='[\u@\h \d \A] \w \$ '
```

Il est aussi possible d'utiliser des variables d'environnement comme `$PWD` mais également de changer les couleurs ou d'ajouter des mises en forme, voir le chapitre « Utiliser de la couleur ».

Voici la liste des différents caractères disponibles :

| Commande		| Signification																						|
| :------------ | :------------------------------------------------------------------------------------------------ |
| \a			| Le caractère ASCII de la sonnerie (007). Sonnera à chaque commande exécutée dans le Terminal.		|
| \A			| Affiche l’heure actuelle au format : HH:MM sur 24 heures.											|
| \d			| Affiche la date actuelle au format : « Jour de la semaine » « Mois » « Jour du mois ».			|
| \D {format}	| Le *format* est passé à `strftime`(3) et son résultat est inséré dans la chaîne d’invite.			|
| \e			| Le caractère ASCII d’échappement (033).															|
| \H			| Le nom d’hôte.																					|
| \h			| Le nom d’hôte jusqu’au premier point « . ».														|
| \j			| Le nombre de tâches actuellement gérées par le *shell*.											|
| \l			| La base du nom du périphérique de Terminal du *shell*.											|
| \n			| Un retour chariot et un saut de ligne.															|
| \r			| Un retour chariot.																				|
| \s			| Le nom du *shell*.																				|
| \T			| L’heure actuelle au format HH:MM:SS sur 12 heures.												|
| \t			| L’heure actuelle au format HH:MM:SS sur 24 heures.												|
| \@			| L’heure actuelle au format HH:MM sur 12 heures (am/pm).											|
| \u			| Le nom de l’utilisateur courant.																	|
| \v			| Le numéro de version du `bash`, par exemple : `2.00`.												|
| \V			| Le numéro de version complet du `bash`, incluant le niveau de correctif, par exemple : `2.00.0`.	|
| \w			| Le répertoire de travail actuel.																	|
| \W			| Le nom de base du répertoire de travail actuel.													|
| \\#			| Le numéro de la commande en cours (sur la session actuelle).										|
| \\!			| Le numéro d’historique de la commande.															|
| \$			| Si l’UID réel est 0, affiche le dièse `#`, sinon le dollar `$`.									|
| \nnn			| Le caractère correspondant au code en octal (007 ou 033 par exemple).								|
| \\\			| Barre oblique inverse.																			|
| \\[			| Début d’une suite de caractères non imprimables, comme des séquences de contrôle du Terminal.		|
| \\]			| Fin d’une suite de caractères non imprimables.													|

Il est à noter que l'option `\D {format}` avec des accolades vides, retournera une représentation de l’heure conformément aux paramètres régionaux du système.

### Utiliser de la couleur

Il est parfois nécessaire d'utiliser de la couleur ou certaines mises en forme (gras, italique, clignotant) afin d'obtenir une meilleure visualisation du résultat, notamment dans les fichiers de log. La commande de base est la suivante :

``` bash
echo -e '\033[A;B;CmUne chaîne de caractères.\033[0m'
```

L'option *e* permet de prendre en compte les paramètres échappés avec les antislashs « \ ». On retrouve ensuite les valeurs A, B et C. A correspond à un effet affecté au texte affiché ; B indique une couleur de texte et enfin C indique la couleur de fond. La séquence `\033[` délimite l'entrée de ces valeurs alors que `\033[0m` clôt ces préférences et revient aux valeurs définies par défaut du Terminal. Respectez à la lettre les points-virgules « ; » et n'utilisez pas d'espaces (uniquement à l'intérieur de votre texte). Il est à noter que la séquence `\033` représente le caractère ASCII d’échappement et le caractère « m » indique une séquence d’échappement de couleur. Le `0m` final permet donc de revenir aux couleurs par défaut.

Avec la commande `printf`, le résultat est identique :

``` bash
printf '\033[A;B;CmUne chaîne de caractères.\033[0m'
```

La valeur de A peut-être remplacée par une des valeurs suivantes :

| Code			| Effet				|
| :------------	| :----------------	|
| 0				| Réinitialisation	|
| 1				| Gras				|
| 21			| Non-gras			|
| 4				| Souligné			|
| 24			| Non Souligné		|
| 5				| Clignotant		|
| 25			| Non clignotant	|
| 7				| Inversé			|
| 27			| Non inversé		|
| 8				| Masqué			|
| 28			| Non masqué		|

Pour les couleurs, il faut utiliser les nombres suivants à la place des valeurs B et C :

| Couleur		| Couleur du texte	| Couleur du fond	|
| :------------ | :---------------: | :---------------:	|
| Noir			| 30				| 40				|
| Rouge			| 31				| 41				|
| Vert			| 32				| 42				|
| Jaune			| 33				| 43				|
| Bleu			| 34				| 44				|
| Magenta		| 35				| 45				|
| Cyan			| 36				| 46				|
| Blanc			| 37				| 47				|

Il est possible de n'indiquer qu'une ou deux valeurs sur les trois, par exemple :

``` bash
echo -e '\033[1mUne chaîne de caractères.\033[0m'
```

D'autres exemples :

``` bash
echo -e '\033[31mAttention :\033[0m Ceci est un message important.'
```

``` bash
echo -e '\033[7;31;30mInformation :\033[0;5m Ceci est une information.\033[0m'
```

### Des étoiles lors de la saisie de mots de passe

Il n'est pas recommandé de réaliser cette manipulation. Effectivement, par défaut, quand une commande vous demande d'entrer un mot de passe, aucun caractère n’est affiché lors de votre saisie. Ceci est tout à fait normal. Pour des raisons de sécurité, l'affichage ne montre pas le nombre de caractères qui composent votre mot de passe. Pour modifier ce comportement, utilisez cette commande :

``` bash
sudo visudo
```

Localisez la ligne suivante :

``` bash
Defaults env_reset
```

Modifiez-la comme ceci :

``` bash
Defaults env_reset,pwfeedback
```

Quittez votre Terminal et relancez-le. Normalement, toute commande vous demandant un mot de passe affiche désormais celui-ci en caractères étoilés.

[UNIX]: http://fr.wikipedia.org/wiki/Unix "Wikipedia : UNIX"
[Cygwin]: http://www.cygwin.com "Cygwin - Site officiel"
[Wikipedia]: http://fr.wikipedia.org/wiki/Cygwin "Wikipedia : Cygwin"
