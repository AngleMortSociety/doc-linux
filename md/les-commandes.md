
# Les commandes

Nous allons passer en revue les commandes les plus courantes qui constituent un système GNU/Linux (quelques différences peuvent néanmoins apparaître selon les systèmes). Toutes ces commandes sont présentes par défaut mais vous pourrez en installer de nouvelles en fonction de vos besoins. De plus, il convient de noter que les options indiquées pour chaque commande ne constituent en aucun cas une liste exhaustive. Il vous sera donc indispensable de lire le *manuel* de chacune afin d'approfondir leur usage.

## Commandes d'informations

### alias
[[Primitive du shell]]

Afficher l'alias demandé dans le Terminal, s'il existe :

``` bash
alias un-alias
```

Pour afficher tous les alias :

``` bash
alias
```

Il est possible de définir de nouveaux alias :

``` bash
alias un-alias="une-commande"
```

Un alias défini dans le Terminal sera détruit lors de la prochaine déconnexion. Pour préserver un alias, il est nécessaire de l'enregistrer dans un fichier `.profile` ou `.bashrc`.

### apropos

Si vous avez oublié le nom d'une commande, `apropos` peut vous aider à la retrouver. Une liste correspondant à ce (ou ces) mot(s) clé(s) sera affichée comme résultat dans le Terminal. La liste peut être longue mais elle vous aidera sûrement à vous rafraîchir la mémoire.

``` bash
apropos mot-clé mot-clé mot-clé
```

Il est possible d'avoir une brève description de la commande (description que l'on retrouve avec la commande `whatis`) :

``` bash
apropos commande
```

### cal
((Calendar))

Affiche le calendrier du mois en cours, la date du jour étant surlignée (pas sur tous les systèmes ou configurations de Terminal). Pour afficher le mois précédent et le suivant en plus du mois en cours, utilisez l'option *3* :

``` bash
cal -3
```

Il est possible de demander le calendrier complet de l'année passée en paramètre :

``` bash
cal 2014
```

Et de préciser le mois :

``` bash
cal 5 2014
```

### cmp
((Compare))

Permet de comparer deux fichiers. Si les fichiers sont identiques, la commande ne retourne rien.

``` bash
cmp fichier-A fichier-B
```

### date
((Date and time))

Affiche le jour et l'heure. Reportez-vous au *manuel* de la commande car beaucoup d'options sont disponibles.

``` bash
date
```

### df
((Disk Free))

Affiche les informations relatives à l'espace disque utilisé par tous les systèmes de fichiers montés.

``` bash
df -HaT --total
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-a*			| *all*			| Affiche les systèmes de fichiers ayant une taille de 0 blocs.		|
| *-h*			| *human*		| Indique la taille des fichiers en Ko, Mo, Go (base 2).			|
| *-H*			| *Human*		| Indique la taille des fichiers en Ko, Mo, Go (base 10).			|
| *-T*			| *Type*		| Affiche le système de fichier.									|
| *--total*		| *total*		| Donne le total de chaque type de données affichées.				|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### du
((Disk Usage))

Permet de connaître la taille occupée par les fichiers et sous-dossiers du chemin indiqué.

``` bash
du -hs chemin
```

Voici les principales options :

| Option 		| Signification	| Détail															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-a*			| *all*			| Affiche tout (par défaut, n'affiche que les sous-dossiers).		|
| *-h*			| *human*		| Indique la taille des fichiers en Ko, Mo, Go.						|
| *-s*			| *simple*		| Donne uniquement le résultat, incompatible avec l'option *a*.		|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### file

Retourne le type du fichier demandé : *directory*, *empty*, *ISO Media*, etc. Lisez attentivement le *manuel*, beaucoup d'options sont disponibles.

``` bash
file fichier
```

### free

Affiche les informations sur la mémoire disponible / utilisée du système.

``` bash
free -hts 10
```

Voici les principales options :

| Option 		| Signification	| Détail 																		|
| :------------	| :------------	| :----------------------------------------------------------------------------	|
| *-h*			| *human*		| Indique la taille des fichiers en Ko, Mo, Go.									|
| *-s* n		| *seconds*		| Affiche, toutes les *n* secondes, le tableau. A vous d'indiquer un temps.		|
| *-t*			| *total*		| Ajoute une ligne qui additionne toutes les valeurs.							|

Utilisez la combinaison de touches <kbd>CTRL</kbd> + <kbd>C</kbd> pour quitter la commande lancée avec l'option *s*.

### groups

Affiche la liste des groupes dont vous faites partie (sans paramètre) ou dont fait partie l'utilisateur demandé (nom de l'utilisateur en paramètre).

``` bash
groups utilisateur
```

### help
[[Primitive du shell]]

Affiche l'aide et liste toutes les *primitives du shell*.

``` bash
help
```

Pour afficher l'aide d'une *primitive du shell* :

``` bash
help primitive-du-shell
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-d*			| *description*	| Affiche une courte description.									|
| *-m*			| *manual*		| Affiche l'aide dans un format proche des pages de manuels.		|
| *-s*			| *synopsis*	| Affiche le synopsis pour utiliser la *primitive du shell*.		|

### id

Affiche vos identifiants, groupes effectifs et réels. Un utilisateur peut-être spécifié en argument.

``` bash
id utilisateur
```

### info
((Info documents))

Alternative de la commande `man`, permet de lire les documentations au format *info*. Appuyez sur la touche <kbd>q</kbd> pour revenir au Terminal.

``` bash
info commande
```

### ls
((List segment))

Affiche la liste des fichiers présents dans le dossier courant ou demandé. Equivalent de la commande `dir` sous Windows.

``` bash
ls -FlAh chemin
```

Voici les principales options :

| Option 		| Signification | Détail 																				|
| :------------	| :------------	| :------------------------------------------------------------------------------------	|
| *-a*			| *all*			| Affiche tous les fichiers, y compris les fichiers cachés.								|
| *-A*			| *Almost all*	| Idem que *a* mais sans les dossiers « . » et « .. »									|
| *-F*			| *classiFy*	| Ajoute un indicateur aux dossiers, exécutables, liens, etc. (* / = > @ &#124;).		|
| *-p*			| 				| Ajoute un indicateur aux dossiers : « / ».											|
| *-l*			| *list*		| Liste détaillée (affiche les droits, la date, l'utilisateur, le groupe, etc.).		|
| *-h*			| *human*		| Indique la taille des fichiers en Ko, Mo, Go.											|
| *-t*			| *time*		| Tri par date de dernière modification (nouveaux en premier).							|
| *-r*			| *reverse*		| Inverse le tri.																		|
| *-R*			| *Recursive*	| Affiche également le contenu de chaque dossier.										|
| *-i*			| *inode*		| Affiche les numéros d'inode, utile pour repérer les liens (voir la commande `ln`).	|

### man
((Manual))

Affiche le *manuel* de la commande demandée. Appuyez sur la touche <kbd>q</kbd> pour quitter et revenir au Terminal.

``` bash
man commande
```

Les principales touches pour le manipuler sont :

| Touche 											| Evènement																										|
| :------------------------------------------------	| :------------------------------------------------------------------------------------------------------------ |
| <kbd>pageDown</kbd> ou <kbd>Espace</kbd>			| Descend d'une page.																							|
| <kbd>pageUp</kbd> ou <kbd>b</kbd>					| Remonte d'une page.																							|
| <kbd>↓</kbd> ou <kbd>j</kbd> ou <kbd>ENTRÉE</kbd>	| Descend d'une ligne.																							|
| <kbd>↑</kbd> ou <kbd>y</kbd>						| Remonte d'une ligne.																							|
| <kbd>q</kbd> ou <kbd>Q</kbd>						| Quitte le *manuel*.																							|
| <kbd>=</kbd>										| Indique le numéro de la première ligne ainsi que celui de la dernière affichée à l'écran.						|
| <kbd>h</kbd> ou <kbd>H</kbd>						| Affiche l'aide, <kbd>q</kbd> pour revenir au *manuel*.														|
| <kbd>/</kbd>										| Lance une recherche. Tapez <kbd>n</kbd> pour afficher le résultat suivant et <kbd>N</kbd> pour le précédent.	|

#### Les sections

Plusieurs sections distinctes peuvent composer un *manuel* :

1. Programmes exécutables ou commandes de l'interpréteur de commandes (*shell*), par défaut c'est cette section qui est retournée.
2. Appels système (fonctions fournies par le noyau)
3. Appels de bibliothèques (fonctions fournies par des bibliothèques utilisables en C)
4. Fichiers spéciaux (situés généralement dans `/dev`)
5. Formats de fichiers et conventions (par exemple `/etc/passwd`)
6. Jeux
7. Divers (y compris les macropaquets et les conventions, par exemple : man(7) ou groff(7))
8. Commandes de gestion du système (généralement réservées au **super user**)
9. Interface du noyau GNU/Linux

Le *manuel* affiché, le numéro de section est souvent spécifié entre parenthèses, après le nom de la commande.

Pour spécifier une section particulière il suffit d'ajouter son numéro, comme ceci :

``` bash
man 7 man
```

De plus, chaque section possède une page appelée *intro* qui la présente, accessible comme les autres pages de *manuel*. Pour lire l'introduction de la section 3, il suffit donc de saisir :

``` bash
man 3 intro
```

#### Organisation

Plusieurs chapitres composent un *manuel* :

- *Name*			: le nom de la commande
- *Synopsis*		: indique comment utiliser la commande (voir ci-dessous)
- *Description*		: explique la commande en détail
- *Options*			: liste et détaille les options
- *Exemples*		: exemples d'utilisation, cette section n'est pas toujours présente
- *Author(s)*		: personnes qui ont participées au développement
- *Reporting bugs*	: adresses pour contacter les personnes quand vous trouvez des bugs
- *Copyright*		: termes qui indiquent la licence utilisée
- *See also*		: voir aussi, d'autres commandes ou pages de *manuel*

D'autres chapitres peuvent être présents mais ceux-ci sont les plus courants.

#### Synopsis

Une mise en forme standardisée explique comment une commande doit-être utilisée, voici le détail :

| Mise en forme				| Détail																								|
| :------------------------	| :---------------------------------------------------------------------------------------------------- |
| **Mot en gras**			| Ecrire le mot tel quel, sans aucune modification, obligatoire (en général le nom de la commande).		|
| <u>Mot souligné</u>		| Doit être remplacé par le nom approprié (le soulignement n'est pas toujours actif).					|
| [OPTIONS]					| Les crochets représentent des options, donc facultatif.												|
| DIRECTORY					| Arborescence requise (chemin absolu ou relatif).														|
| ...						| Signifie que l'on peut répéter plusieurs fois le mot clé précédent.									|

#### Extensions et traductions

Il est possible d'installer des paquets supplémentaires pour avoir, par exemple, les pages de *manuel* en français :

- *manpages-fr*			: version française des pages de manuel pour l'utilisation de GNU/Linux
- *manpages-fr-extra*	: version française des pages de manuel concernant les programmes
- *manpages*			: pages de manuel (en anglais) pour l'utilisation de GNU/Linux
- *manpages-posix*		: pages de manuel (en anglais) pour l'utilisation des systèmes POSIX

Pour les développeurs :

- *manpages-fr-dev*		: version française des pages de manuel pour les développeurs
- *manpages-dev*		: pages de manuel (en anglais) pour les développeurs
- *manpages-posix-dev*	: pages de manuel (en anglais) sur l'utilisation des systèmes POSIX pour les développeurs

Autre :

- *funny-manpages*		: pages de manuel humoristique (en anglais)

Si vous installez une version *fr* pour les *manuels*, il est toujours bon d'avoir en plus les versions originales en anglais. Pour ce faire utilisez l'option *L* (pour *Locate*), comme ceci :

``` bash
man -L en cp
```

### pwd
[[Primitive du shell]] ((Print working directory))

Affiche le chemin absolu du répertoire courant.

``` bash
pwd
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### stat

Affiche les informations concernant le fichier spécifié : dernière date d'accès, de modification ou de création, taille, etc.

``` bash
stat fichier
```

### tty

Affiche le nom de fichier du Terminal relié à l'entrée standard, autrement dit le numéro du Terminal où vous êtes connecté.

``` bash
tty
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-s*			| *silent*		| N'affiche rien, retourne uniquement la valeur de retour.			|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### type
[[Primitive du shell]]

Indique si la commande donnée en paramètre est une *primitive du shell*, un alias ou autre. Le chemin où se trouve la commande peut-être retourné.

``` bash
type commande
```

### uname

Pour obtenir des informations sur le système. Pour un retour complet utilisez l'option *a* :

``` bash
uname -a
```

### uptime

Affiche l'heure actuelle, la durée depuis laquelle le système fonctionne, le nombre d'utilisateurs actuellement connectés et la charge système moyenne.

``` bash
uptime
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### users

Affiche les utilisateurs actuellement connectés au système.

``` bash
users
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### w
((Who))

Globalement, même chose que la commande `who`. L’en-tête affiche, dans cet ordre, l’heure actuelle, le temps d'activité du système (*up*), le nombre d’utilisateurs actuellement connectés et la charge moyenne pour la dernière, les 5 et les 15 dernières minutes. Les entrées suivantes sont affichées pour chacun des utilisateurs : nom d’utilisateur, nom du terminal (« tty » ou « pts »), nom de l'hôte distant, l'heure de la connexion, le temps d’inactivité, le JCPU, le PCPU qui indique le temps d'exécution du processus en cours et, enfin, le nom de ce dernier.

``` bash
w
```

### whatis
((What is))

Retourne une brève description d'une commande (description que l'on retrouve avec la commande `apropos`) :

``` bash
whatis commande
```

### whereis
((Where is))

Localise les commandes (source ou binaire) et la section de leurs manuels.

``` bash
whereis commande
```

Voici les principales options :

| Option 		| Signification	| Détail 								|
| :------------	| :------------	| :------------------------------------	|
| *-b*			| *binaire*		| Recherche uniquement les binaires.	|
| *-m*			| *manual*		| Recherche uniquement les manuels.		|
| *-s*			| *source*		| Recherche uniquement les sources.		|

### which

Très utile quand vous cherchez à localiser une commande (fichier binaire) ou un script (fichier exécutable). `which` parcourt la variable globale PATH et vous affiche le résultat. Attention toutefois, vous devez disposer des droits d'exécution pour que le résultat s'affiche. Si vous n'obtenez rien en retour, c'est que la commande (ou le script) n'est pas installée sur votre système ou que vous ne disposez pas de droits suffisants pour voir le résultat. Utile pour voir rapidement si une commande est disponible.

``` bash
which commande
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-a*			| *all*			| Affiche tous les chemins correspondant à chaque argument.			|

### who
((Who))

Affiche les informations sur les utilisateurs actuellement connectés.

``` bash
who -H
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-a*			| *all*			| Affiche toutes les informations.									|
| *-b*			| *boot*		| Indique la date et l'heure du dernier démarrage de la machine.	|
| *-H*			| *Head*		| Ajoute l'intitulé de chaque colonne du tableau affiché.			|

### whoami
((Who am i))

Affiche votre login de connexion.

``` bash
whoami
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

## Naviguer dans l'arborescence

### cd
[[Primitive du shell]] ((Change directory))

Permet de se déplacer dans l'arborescence du système.

``` bash
cd chemin
```

Voici quelques exemples d'interactions :

| Commande 		| Signification															|
| :------------	| :-------------------------------------------------------------------- |
| `cd`			| Revient directement dans le dossier *home* de l'utilisateur courant.	|
| `cd ~`		| Idem.																	|
| `cd -`		| Revient au dossier précédemment visité.								|
| `cd ~login`	| Permet de se déplacer dans un dossier utilisateur.					|
| `cd /`		| Racine du système.													|
| `cd ..`		| Remonte au dossier parent.											|
| `cd ../..`	| Remonte de deux dossiers parents.										|
| `cd chemin`	| Permet de se déplacer à l'endroit voulu (chemin absolu ou relatif).	|

## Editeurs de texte

Plusieurs commandes permettent d'éditer des fichiers texte. On trouve notament les commandes `vi` et `nano`, généralement installées sur tous les systèmes. D'autres sont très connues et utilisées par la communauté comme `emacs` ou `vim`. Cette dernière fait d'ailleurs l'objet d'un chapitre complet.

### emacs
((Editing MACroS running on TECO))

Editeur de texte très puissant. Cette commande n'est généralement pas installée sur les distributions GNU/Linux mais elle mérite d'être signalée car elle est très puissante.

### nano
((Nano's ANOther editor))

Vous pouvez le lancer en précisant le nom du fichier à créer ou à ouvrir :

``` bash
nano fichier
```

Voici les principales options :

| Option 		| Signification	| Détail 																	|
| :------------	| :------------	| :------------------------------------------------------------------------	|
| *-B*			| *Backup*		| Un autre fichier, avec le suffixe *~*, sera créé à chaque sauvegarde.		|
| *-E*			| *tabstospaces*| Converti les tabulations en espaces.										|
| *-c*			| *const*		| Affiche constamment la position du curseur.								|
| *-i*			| *autoindent*	| Indente les nouvelles lignes, très utile pour l'édition de code.			|
| *-m*			| *mouse*		| Active le support de la souris.											|
| *-v*			| *view*		| Ouvre le fichier en lecture seule.										|

Une fois `nano` ouvert, un menu en bas de l'écran vous indique les touches de raccourcis. Le symbole « ^ » représente la touche <kbd>CTRL</kbd>.

| Raccourci							| Détail																				|
| :--------------------------------	| :------------------------------------------------------------------------------------	|
| <kbd>CTRL</kbd> + <kbd>A</kbd>	| Envoi le curseur au début de la ligne.												|
| <kbd>CTRL</kbd> + <kbd>E</kbd>	| Envoi le curseur à la fin de la ligne.												|
| <kbd>CTRL</kbd> + <kbd>Y</kbd>	| Remonte d'une page.																	|
| <kbd>CTRL</kbd> + <kbd>V</kbd>	| Descend d'une page.																	|
| <kbd>CTRL</kbd> + <kbd>_</kbd>	| Permet de se rendre aux numéros de ligne et colonne indiquées.						|
| <kbd>CTRL</kbd> + <kbd>C</kbd>	| Affiche les numéros de ligne, colonne et caractère à partir de la position du curseur.|
| <kbd>CTRL</kbd> + <kbd>W</kbd>	| Pour lancer une recherche.															|
| <kbd>CTRL</kbd> + <kbd>D</kbd>	| Supprime un caractère.																|
| <kbd>CTRL</kbd> + <kbd>K</kbd>	| Coupe la ligne.																		|
| <kbd>CTRL</kbd> + <kbd>U</kbd>	| Colle.																				|
| <kbd>CTRL</kbd> + <kbd>O</kbd>	| Sauvegarde un fichier.																|
| <kbd>CTRL</kbd> + <kbd>X</kbd>	| Quitte `nano` ou son aide.															|
| <kbd>CTRL</kbd> + <kbd>G</kbd>	| Affiche l'aide, <kbd>CTRL</kbd> + <kbd>X</kbd> pour revenir au fichier.				|

#### configuration

Pour configurer `nano`, il est conseillé de copier le fichier `nanorc` dans le dossier home :

``` bash
cp /etc/nanorc ~/.nanorc
```

Ouvrez ce fichier qui propose beaucoup de réglages et qui sont, pour la plupart, commentés avec le symbole dièse « # ». Supprimez-les pour activer les options choisies. Il faudra relancer `nano` pour prendre en compte les modifications si vous éditez ce fichier avec celui-ci.

### vi
((Visual Interface))

Autre éditeur de texte très puissant. Reportez-vous à la commande `vim` pour plus de détails.

### vim
((Vi IMproved))

Evolution de `vi`, reportez-vous au chapitre qui lui est consacré. C'est le clone le plus populaire de `vi` mais il n'est pas toujours installé par défaut sur les distributions GNU/Linux.

## Visualiser le contenu d'un fichier

Il est souvent nécessaire dans un Terminal de lire le contenu d'un fichier. Dans ce cas, des programmes légers et dédiés à cette tâche existent, nous allons les découvrir ici.

### cat
((Concatenate))

Affiche le contenu d'un ou plusieurs fichiers (dans ce cas, on concatène) en un seul bloc, les numéros de lignes sont indiqués avec l'option *n* (pour *number*).

``` bash
cat -n fichier-A fichier-B
```

### head

Pour visualiser l'en-tête d'un fichier. Il est possible d'indiquer le nombre de lignes à afficher avec l'option *n* (la valeur par défaut étant de 10), l'option *v* (pour *verbose*) indiquera le nom du fichier demandé.

``` bash
head -vn3 fichier
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-c* n		| 				| Affiche les *n* premiers caractères du fichier.					|
| *-n* n		| 				| Affiche les *n* premières lignes du fichier.						|
| *-q*			| *quiet*		| Les noms de fichiers ne sont jamais affichés.						|
| *-v*			| *verbose*		| Les noms de fichiers sont toujours affichés.						|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### less

Cette commande affiche l'intégralité du fichier, on peut ensuite effectuer plusieurs opérations. Regardez le *manuel* de cette commande, beaucoup d'options sont disponibles.

``` bash
less fichier
```

Voici les principales touches pour interagir avec le fichier affiché :

| Touche 											| Evènement																										|
| :------------------------------------------------	| :------------------------------------------------------------------------------------------------------------ |
| <kbd>pageDown</kbd> ou <kbd>Espace</kbd>			| Descend d'une page.																							|
| <kbd>pageUp</kbd> ou <kbd>b</kbd>					| Remonte d'une page.																							|
| <kbd>↓</kbd> ou <kbd>j</kbd> ou <kbd>ENTRÉE</kbd>	| Descend d'une ligne.																							|
| <kbd>↑</kbd> ou <kbd>y</kbd>						| Remonte d'une ligne.																							|
| <kbd>q</kbd> ou <kbd>Q</kbd>						| Quitte le programme.																							|
| <kbd>=</kbd>										| Indique le numéro de ligne, le pourcentage parcouru, etc.														|
| <kbd>h</kbd> ou <kbd>H</kbd>						| Affiche l'aide, <kbd>q</kbd> pour revenir au contenu du fichier.												|
| <kbd>/</kbd>										| Lance une recherche. Tapez <kbd>n</kbd> pour afficher le résultat suivant et <kbd>N</kbd> pour le précédent.	|

### more

Equivalent de la commande `less`, la différence est que le contenu du fichier est directement affiché dans le Terminal et que la commande vous rend la main.

``` bash
more fichier
```

### nl
((Number lines))

Affiche le contenu des fichiers texte passés en arguments en numérotant chaque ligne.

``` bash
nl fichier
```

### tac
((Etanetacnoc))

Même principe que la commande `cat`, affiche les fichiers dans l'ordre demandé en inversant leur contenu.

``` bash
tac fichier-A fichier-B
```

### tail

Cette commande est l'inverse de `head` car elle permet de visualiser la fin d'un fichier. Grâce à l'option *f* (pour *follow*), elle permet de suivre l'évolution d'un fichier en temps réel, très pratique pour suivre des logs. Tout comme la commande `head`, avec l'option *n*, il est possible de spécifier le nombre de lignes affichées (la valeur par défaut étant de 10). Dans le cas d'un suivi de fichier (option *f*), le Terminal ne rend pas la main. Dans ce cas, pour revenir à la ligne de commande, utilisez la combinaison de touches <kbd>CTRL</kbd> + <kbd>C</kbd>.

``` bash
tail -fn3 fichier
```

## Manipulation des fichiers

### cp
((Copy))

Permet de copier des fichiers ou des dossiers. On peut ainsi dupliquer un fichier :

``` bash
cp fichier-A fichier-B
```

Le copier dans un autre dossier :

``` bash
cp fichier chemin/dossier/
```

Bien sûr, on peut lui donner un nouveau nom :

``` bash
cp fichier-nom chemin/dossier/fichier-nouveau-nom
```

Copier un dossier (et son contenu) nécessite l'option *R* ou *r* (pour *Recursive*) :

``` bash
cp -r chemin/dossier/ chemin/autre-dossier/
```

### ln
((Link))

Il existe deux types de liens sous un système GNU/Linux :

- Les liens *physiques*
- Les liens *symboliques*

Tout d'abord, les liens physiques. Ils permettent de créer une entrée vers un fichier. Ceci permet d'avoir accès à un même fichier à des endroits différents du système et éventuellement avec des noms distincts (en interne, Linux enregistre les fichiers sur la base d'un numéro d'inode et non pas sur la base d'un nom). Un fichier ne sera alors réellement effacé que lorsqu'aucun lien physique ne pointera vers ce dernier. Il n'y a pas de notion de nom « original ».

``` bash
ln fichier lien-fichier
```

Les liens symboliques sont l'équivalent des raccourcis que l'on trouve dans Windows. Le lien ne pointe plus sur l'inode du fichier mais vers son nom. Ainsi, si vous supprimez ou renommez le fichier pointé, le lien se cassera et rien ne se produira quand vous voudrez y accéder. Ce type de lien est très utilisé pour accéder à des dossiers, ce qui est aussi possible avec les liens physiques mais un peu plus compliqué. Pour un lien *symbolique*, utilisez l'option *s* (pour *symbolic*) :

``` bash
ln -s fichier lien-fichier
```

Pour connaître le nombre de liens qui pointent vers un fichier, il suffit d'utiliser la commande `ls -l` pour avoir le détail.

### mkdir
((Make directories))

Commande pour créer des dossiers.

``` bash
mkdir dossier
```

On peut en créer plusieurs avec une seule ligne de commande :

``` bash
mkdir dossier1 dossier2 chemin/dossier3
```

Ou créer une arborescence complète avec l'option *p* (pour *parents*) :

``` bash
mkdir -p chemin/dossier/sous-dossier1/sous-dossier2
```

Une option intéressante, *m* (pour *mode*), reprend le principe de la commande `chmod`. A la création, on choisit les droits du dossier :

``` bash
mkdir -m 777 dossier
```

### mv
((Move)) ((Rename))

Cette commande est destinée à deux usages, l'usage classique est de déplacer un fichier ou un dossier :

``` bash
mv fichier dossier-de-destination/fichier
```

L'autre possibilité est de renommer un fichier ou un dossier. Effectivement, il n'existe pas de commande dédiée à cet usage :

``` bash
mv fichier-A fichier-B
```

### rcp

Cette commande permet de copier des fichiers entre deux machines distantes. Préférez plutôt `scp` couplée à un tunnel `ssh` pour plus de sécurité.

### readlink
((Read link))

Affiche la valeur d'un lien symbolique ou le nom canonique d'un fichier.

``` bash
readlink lien
```

### rm
((Remove))

Efface des fichiers ou des dossiers.

``` bash
rm fichier-A fichier-B
```

Voici les principales options :

| Option 		| Signification	| Détail 										|
| :------------	| :------------	| :--------------------------------------------	|
| *-i*			| *interactive*	| Demande une confirmation pour chaque fichier.	|
| *-f*			| *force*		| Comportement inverse.							|
| *-v*			| *verbose*		| Affiche chaque action.						|
| *-r* ou *-R*	| *recursive*	| Supprime le dossier et son contenu.			|

### rmdir
((Remove directories))

Commande dédiée à la suppression de dossier. Une contrainte forte est liée à l'utilisation de celle-ci, le dossier doit-être vide pour être supprimé. Préférez la commande `rm` avec l'option *r* ou *R* (pour *Recursive*) qui permet de détruire les dossiers non-vides.

``` bash
rmdir chemin/dossier-vide/
```

### rsync

Cette commande permet de synchroniser deux dossiers, c'est l'idéal pour réaliser des sauvegardes. La commande de base qui permet de copier un dossier dans un autre est la suivante :

``` bash
rsync -a dossier-origine dossier-2-destination
```

Pour copier le contenu du premier dossier dans le second, il faut ajouter un slash :

``` bash
rsync -a dossier-origine/ dossier-2-destination
```

Pour synchroniser votre dossier sur un disque dur distant (via le réseau, un NAS par exemple), il faut passer par un tunnel `ssh` :

``` bash
rsync -ae ssh dossier-origine/ user@adresseIP:/dossier-2-destination
```

L'option *a* (pour *archive*) préserve les informations des fichiers copiés avec `rsync` et réalise une copie récursive de votre arborescence (copie des liens symboliques, préservation des permissions, dates de modifications, groupes et utilisateurs).

Le *e* est réservé pour la connexion `ssh`. Notez que dans le cas d’une copie sur un autre serveur, la commande `rsync` doit s’y trouver. De plus, les deux commandes doivent avoir la même version. Bien sûr, il vous faudra les droits d’écriture sur le dossier de destination avec le compte que vous utiliserez. Vous pouvez automatiser ce genre de commande en écrivant ces lignes dans un script qui peut être inclus dans une `crontab`. Dès lors, il sera utile de créer un couple de clés publiques/privées pour se connecter avec `ssh` sans avoir à entrer le mot de passe, auquel cas le script deviendrait bien moins intéressant car nécessitant toute votre attention.

Détailler `rsync` avec précision exigerait l'écriture d’un ouvrage complet. Lisez le `man`, interrogez Google, naviguez dans les forums : vous découvrirez qu’une multitude de possibilités existe avec cette commande.

### scp
((Secure copy))

A l'image de la commande `cp`, celle-ci permet de copier des fichiers ou des dossiers entre deux machines à travers une connexion `ssh` et donc, de manière sécurisée. Pour plus d'informations, reportez-vous au chapitre `ssh` qui détaille cette commande.

Pour copier un fichier de manière sécurisée entre deux machines :

``` bash
scp -P 910 fichier login@adresse-ip:dossier-de-destination
```

Notez que l'option *P* (pour *Port*) diffère de l'option `ssh` *p*. Il est nécessaire d'indiquer le dossier de destination sur la machine distante. Un point peut être utilisé afin de copier le fichier à la racine du dossier *home* de l'utilisateur.

A l'inverse, pour récupérer un fichier sur la machine distante :

``` bash
scp -P 910 login@adresse-ip:dossier/fichier dossier-de-destination/fichier
```

Voici les principales options :

| Option 		| Signification	| Détail																					|
| :------------	| :------------	| :----------------------------------------------------------------------------------------	|
| *-P*			| *Port*		| Permet de spécifier le port de connexion `ssh`.											|
| *-p*			| *preserves*	| Préserve les dates de modifications et d'accès ainsi que les droits du fichier original.	|
| *-q*			| *quiet*		| Masque la barre de progression ainsi que tous les autres messages.						|
| *-r*			| *recursive*	| Copie les dossiers et leurs contenus de manière récursive.								|
| *-v*			| *verbose*		| Affiche les messages en mode *debug* pour localiser les problèmes de connexion.			|

### split

La commande `split` permet de découper un fichier en plusieurs parties. Cela peut être utile afin de le transporter sur des supports de faible capacité par exemple.

``` bash
split -b 1440k fichier
```

En fonction de la taille du fichier d'origine, un certain nombre de fichiers seront créés et ainsi nommées : xaa, xab, xac, etc. A part le dernier morceau qui peut être inférieur, ces fichiers feront tous 1440 Ko.

Pour reconstituer le fichier d'origine, il suffit d'utiliser la commande `cat` :

``` bash
cat xa[a-c] > fichier
```

Une autre possibilité :

``` bash
cat xa? > fichier
```

### touch

Cette commande a deux fonctions : soit le fichier que vous "touchez" existe déjà et vous pouvez alors modifier sa date d'accès et de modification, soit il n'existe pas et il est alors créé.

``` bash
touch fichier
```

Utilisée de cette façon, la commande permet de changer les dates d'accès et de modifications du fichier par la date et l'heure où la commande est exécutée. Il est possible de modifier / créer plusieurs fichiers en une seule ligne de commande :

``` bash
touch fichier-A fichier-B
```

Pour modifier un fichier à une date précise, il est nécessaire d'utiliser l'option *d* (pour *date*) et d’indiquer tous les composants de la date souhaitée :

``` bash
touch -d AAAAMMJJ fichier
```

La commande précédente modifie les dates par celle indiquée ; l’heure est, quant à elle, initialisée à 0. L'option *t* (pour *time*), permet de changer à la fois la date et l'heure, comme ici (changement uniquement sur la date de modification avec l’option *–m*) :

``` bash
touch -mt AAAAMMJJhhmm fichier
```

AAAAMMJJhhmm se décompose de la façon suivante :
- AAAA : l'année souhaitée
- MM : le mois
- JJ : le jour
- hh : l'heure
- mm : les minutes
- ss : les secondes (optionnel avec l'option *-t*)

Voici les principales options :

| Option 		| Signification			| Détail 																|
| :------------	| :--------------------	| :-------------------------------------------------------------------- |
| *-d*			| *date*				| Permet de changer la date : AAAAMMJJ (l'heure sera initialisée à 0).	|
| *-t*			| *time*				| Permet de changer la date et l'heure : AAAAMMJJhhmm(ss).				|
| *-a*			| *access time*			| Change uniquement la date d'accès du fichier.							|
| *-c*			| *no create*			| Aucun fichier ne sera créé.											|
| *-m*			| *modification time*	| Change uniquement la date de modification du fichier.					|
| *--help*		| *help*				| Affiche l'aide de la commande.										|
| *--version*	| *version*				| Indique la version actuellement installée sur le système.				|

## Manipulation de texte

### awk

La commande `awk` permet de produire, manipuler et modifier des fichiers texte. Cette commande étant très puissante, reportez-vous à son *manuel* pour plus d'informations.

### cut

Supprime du contenu dans les fichiers texte.

### grep

Recherche une chaîne de caractère dans un fichier. S'il n'y a pas de retour dans le Terminal, alors aucun résultat ne correspond à votre recherche.

``` bash
grep "chaine de caractère" fichier
```

Voici les principales options :

| Option 		| Signification	| Détail 														|
| :------------	| :------------	| :------------------------------------------------------------	|
| *-i*			| *ignore case*	| Ne prend pas en compte la casse.								|
| *-n*			| *number*		| Affiche le numéro de ligne de chaque correspondance.			|
| *-v*			| *invert match*| Inverse le résultat demandé dans la chaine de caractère.		|
| *-r*			| *recursive*	| Recherche dans les sous-dossiers.								|
| *-E*			| *Extended*	| Permet d'utiliser les expressions régulières (voir `egrep`).	|

### join

Permet de fusionner les lignes de deux fichiers ayant un champ commun. Elle effectue des jointures (dans le sens d'une base de données relationnelle) entre les deux fichiers texte passés en argument. Prenons le cas de ces deux fichiers :

``` bash
# fichierPrenom
ID_1 Jean
ID_2 Luc
ID_3 Maurice

# fichierNom
ID_1 DUPOND
ID_2 DUCHAMPS
ID_3 BELMON
```

Comme la clé (le ID) est au début de chaque fichier, il n'est pas nécessaire de l'indiquer à la commande. Il suffit de passer en paramètre les fichiers :

``` bash
join fichierPrenom fichierNom > fichierFinal
```

Dans le cas des fichiers suivants :

``` bash
# fichierPrenom
ID_1 Jean
ID_2 Luc
ID_3 Maurice

# fichierNom
DUPOND		ID_1
DUCHAMPS	ID_2
BELMON		ID_3
```

Il faudra indiquer à la commande, pour chaque fichier, le numéro de la colonne où trouver l'information, comme ceci :

``` bash
join -11 -22 fichierPrenom fichierNom > fichierFinal
```

Le 11 indique : premier fichier, première colonne. Le 22 indique : deuxième fichier, deuxième colonne. Le résultat obtenu avec les deux exemples précédents sera identique à celui-ci :

``` bash
# fichierFinal
Jean DUPOND
Luc DUCHAMPS
Maurice BELMON
```

### sed
((Stream editor))

Permet de réaliser des manipulations avec des expressions rationnelles (*regex*) sur des fichiers texte. Cette commande étant très puissante, reportez-vous à son *manuel* pour plus d'informations.

### sort

Permet de trier les lignes contenues dans un fichier, par défaut le résultat est affiché dans le Terminal. Utilisez alors l'option *o* (pour *output*) si vous souhaitez que le résultat soit écrit dans un fichier de sortie.

``` bash
sort fichier -o fichier-de-sortie
```

Voici les principales options :

| Option 		| Signification	| Détail 																|
| :------------	| :------------	| :--------------------------------------------------------------------	|
| *-o* fichier	| *output*		| Ecrit le résultat dans un fichier de sortie, le nom doit être précisé.|
| *-n*			| *numeric*		| Tri numérique du résultat.											|
| *-R*			| *Random*		| Ordre aléatoire.														|
| *-r*			| *reverse*		| Inverse l'ordre du tri.												|
| *-u*			| *unique*		| Rend unique les résultats, évite de passer par la commande idoine.	|

### tr
((Translate)) ((Delete))

Transpose ou supprime des caractères. Il faut envoyer le fichier à traiter à la commande.

``` bash
tr mot-cherché nouveau-mot < fichier
```

### uniq

Affiche le contenu du fichier dans le Terminal en supprimant les doublons. Cependant, faites attention, le fichier doit d'abord être trié. Si des doublons persistent à des endroits différents, ils seront alors retournés.

``` bash
uniq fichier
```

Utilisez le pipe « &#124; » pour trier vos données avant la commande `uniq`, comme ceci (ou voir la commande `sort -u fichier`) :

``` bash
sort fichier | uniq
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-c*			| *count*		| Préfixe les lignes par le nombre d'occurrences.					|
| *-d*			| *repeated*	| Affiche uniquement les doublons.									|
| *-i*			| *ignore-case*	| Ne prend pas en compte la casse.									|
| *-u*			| *unique*		| N'affiche que les lignes uniques.									|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### wc
((Word count))

Affiche, dans l'ordre : le nombre de lignes d'un fichier, le nombre de mots et le nombre d'octets.

``` bash
wc fichier
```

Voici les options disponibles :

| Option 		| Signification			| Détail 														|
| :------------	| :--------------------	| :------------------------------------------------------------	|
| *-c*			| *bytes*				| Compte les octets.											|
| *-m*			| *char*				| Compte les caractères.										|
| *-l*			| *lines*				| Compte le nombre de lignes d'un fichier, y compris les vides.	|
| *-L*			| *max-lines-lenght*	| Affiche le nombre de caractères de la plus longue ligne.		|
| *-w*			| *words*				| Compte les mots.												|
| *--help*		| *help*				| Affiche l'aide de la commande.								|
| *--version*	| *version*				| Indique la version actuellement installée sur le système.		|

## Commandes pour la console

### clear

Remonte l'invite de commande tout en haut du Terminal, nettoie l'écran de toute information. La combinaison de touches <kbd>CTRL</kbd> + <kbd>L</kbd> donne le même résultat.

``` bash
clear
```

Pas d'option pour cette commande.

### env
((Environment))

Affiche le contenu des variables d'environnement du système. Permet aussi de lancer des programmes avec des environnements modifiés, reportez-vous au *manuel* pour plus d'informations.

``` bash
env
```

### exit
[[Primitive du shell]]

La commande `exit` permet de quitter le Terminal sauf dans le cas où un utilisateur est substitué avec `sudo su` : la commande permet alors de revenir à l'utilisateur courant. Le raccourci clavier <kbd>CTRL</kbd> + <kbd>D</kbd> produit le même résultat. Sur certains systèmes, ce raccourci quitte le Terminal.

``` bash
exit
```

### history
[[Primitive du shell]]

Affiche toutes les commandes précédemment utilisées, numérotées par ordre d'exécution.

``` bash
history
```

Pour exécuter à nouveau la commande numéro 32 :

``` bash
!32
```

Pour exécuter à nouveau la commande `find` la plus récente de l'historique et avec ses paramètres associés :

``` bash
!find
```

Pour afficher les *n* dernières commandes :

``` bash
history 6
```

### logout
[[Primitive du shell]]

Permet de se déconnecter du Terminal. Le raccourci <kbd>CTRL</kbd> + <kbd>D</kbd> produit le même résultat.

``` bash
logout
```

### reset

Réinitialise le Terminal. Parfois, il est possible que le Terminal ait des problèmes d'affichage. Dans ce cas, cette commande peut régler ce problème.

``` bash
reset
```

## Recherche de fichiers

### find

Commande par excellence pour rechercher tout type de fichier. Plus puissante mais aussi, généralement, plus longue à l'exécution que `locate` (en fonction des options que vous indiquez). Son fonctionnement de base est :

``` bash
find <où ?> <quoi ?> <que faire avec ?>
```

#### Où ?

Par défaut, `find` recherche dans le dossier courant et ses sous-dossiers, c'est à dire là où vous l'exécutez. Pour rechercher dans un autre endroit du disque dur, il suffit simplement d'indiquer le chemin (relatif ou absolu).

#### Quoi ?

Le nom du fichier que vous recherchez, il ne faut pas oublier l'option *name* (ou *iname* pour ne pas tenir compte de la casse) :

``` bash
find . -name nom-fichier
```

#### Que faire avec ?

Il est possible de lancer une commande sur les fichiers trouvés. Pour ce faire, il faut utiliser l'option *exec*.

``` bash
find . -name index.html -exec cp {} ./documents/ \;
```

On recherche le fichier *index.html* et avec l'option *exec*, on précise la commande, ici `cp` que l'on souhaite utiliser. Les accolades représentent la liste des fichiers trouvés et on précise où l'on souhaite les copier. Pour terminer, il ne faut pas oublier le point-virgule précédé d'un anti-slash : « \; ».

L'option *ok* demande une confirmation avant chaque action.

``` bash
find . -name index.html -ok -exec cp {} ./documents/ \;
```

#### Des exemples

Recherche dans le *home* de l'utilisateur un fichier de plus de 10 Mo (k: Ko / M: Mo / G: Go)

``` bash
find ~ -size +10M
```

Recherche précisément un fichier de 10Mo (ni plus, ni moins)

``` bash
find ~ -size 10M
```
 
Recherche uniquement des dossiers (*f* pour les fichiers). Par défaut, la commande recherche des dossiers et des fichiers.

``` bash
find ~ -type d -name nom-fichier
```

Pour limiter la recherche aux fichiers vides :

``` bash
find -empty
```

Affiche toutes les informations sur les fichiers trouvés (notez que l'option *ls* doit se trouver à la fin)

``` bash
find -name index.html -ls
```

#### autres options

| Option 		| Détail 																					|
| :------------	| :----------------------------------------------------------------------------------------	|
| *-cmin* -1440	| Recherche les fichiers modifiés ces dernières 24H.										|
| *-cmin* +1440	| Recherche les fichiers modifiés au-delà des dernières 24H.								|
| *-daystart*	| Utilisé avec *ctime*, ne passe pas la journée précédente mais reste sur celle en cours.	|
| *-atime* -n	| Sélectionne les fichiers dont la date d'accès a été changée ces dernières n*24H.			|
| *-ctime* -n	| Sélectionne les fichiers dont la date de statut a été changé ces dernières n*24H.			|
| *-mtime* -n	| Sélectionne les fichiers dont la date de modification a été changé ces dernières n*24H.	|

##### Quelques précisions s'imposent :

- *-atime*		: principalement pour vérifier les accès en lecture d'un fichier.
- *-ctime*		: globalement, prend en compte n'importe quel changement sur le fichier.
- *-mtime*		: modification directe du fichier, son contenu a été modifié.

#### manipulation des résultats

- `find -name "*.jpg" -printf "%p - %u"`		: formate le résultat.
- `find -name "*.jpg" -delete`					: suppression sans confirmation.
- `find -name "*.jpg" -exec chmod 600 {} \;`	: exécute une commande.

### locate

L'avantage de cette commande sur `find` est qu'elle est très rapide car elle fonctionne avec une base de données. Attention toutefois, cette commande n'est pas toujours installée par défaut sur le système.

``` bash
locate fichier
```

Son principal défaut est que si vous créez un fichier et lancez une recherche immédiatement après, il lui sera inconnu et donc, introuvable. Pour y remédier, il faut mettre à jour la base de données :

``` bash
sudo updatedb
```

## Compression / Décompression

### bunzip2

Compresse / décompresse les archives au format *bz2*.

### bzip2

Même chose que `gzip`, plus lent mais compresse davantage.

### compress

Permet de compresser des données, cette commande n'est pas disponible sur certaines distributions GNU/Linux.

### gunzip

Compresse / décompresse les archives au format *gzip* mais aussi les fichiers compressés avec `pack` et `compress`.

### gzip

Compresse / décompresse un fichier.

### tar
((Tape archiver))

Cette commande est utilisée pour archiver des données. Quand on souhaite compresser des informations, archiver avec `tar` est une étape préparatoire.

``` bash
tar -cvf nom-de-l-archive.tar fichier-A fichier-B fichier-C
```

Même commande quand on souhaite archiver un dossier. Il est recommandé de procéder ainsi et de préparer tous les fichiers à archiver dans un dossier spécifique :

``` bash
tar -cvf nom-de-l-archive.tar dossier-contenant-les-fichiers/
```

Voir le contenu d'une archive :

``` bash
tar -tf nom-de-l-archive.tar
```

Pour ajouter un ou plusieurs fichiers dans une archive :

``` bash
tar -tfa nom-de-l-archive.tar fichier-A fichier-B fichier-C
```

Pour extraire les données, il suffit d'écrire ceci :

``` bash
tar -xvf nom-de-l-archive.tar -C dossier-de-destination/
```

Voici les principales options :

| Option 				| Signification	| Détail 											|
| :--------------------	| :------------	| :------------------------------------------------	|
| *-c*					| *create*		| Option obligatoire pour créer un fichier *tar*.	|
| *-v*					| *verbose*		| Affiche les détails de l'opération en cours.		|
| *-f*					| *file*		| Option obligatoire pour préciser les fichiers.	|
| *-t*					| *list*		| Permet de lister les fichiers d'une archive.		|
| *-a*					| *append*		| Ajoute des fichiers dans une archive.				|

On a vu plus haut les commandes de compression. Il est possible d'utiliser cette commande pour archiver et compresser, dans le même temps, une archive.

#### Compression avec gzip (fichier-final.tar.gz ou fichier-final.tgz)

La création s'effectue de cette manière :

``` bash
tar -zcvf nom-de-l-archive.tar.gz dossier-contenant-les-fichiers/
```

L'extraction utilise les options suivantes :

``` bash
tar -zxvf nom-de-l-archive.tar.gz
```

#### Compression avec bzip2 (fichier-final.tar.bz2)

Remarques : `bzip2` crée des fichiers beaucoup plus petits que `gzip` mais utilise plus de ressources processeur, surtout pour compresser.

La création s'effectue de cette manière :

``` bash
tar -jcvf nom-de-l-archive.tar.bz2 dossier-contenant-les-fichiers/
```

L'extraction utilise les options suivantes :

``` bash
tar -jxvf nom-de-l-archive.tar.bz2
```

## Lire des fichiers textes compressés

Des fichiers textes compressés avec les commandes `compress`, `pack` ou `gzip`, peuvent être consultés avec une des commandes suivantes (fonctionne aussi sur des fichiers texte classiques).

### zcat

Même principe que la commande `cat`.

### zless

Même principe que la commande `less`.

### zmore

Même principe que la commande `more`.

## Réseau

### curl

Il s’agit d’un outil pour transférer des données entre deux serveurs en utilisant un des protocoles supportés (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET et TFTP). Pour l'utiliser et télécharger un document :

``` bash
curl 
```

Regardez le *manuel* de cette commande, beaucoup d'options sont disponibles. Notez qu’il existe une autre commande plus puissante mais qui n'est pas installée par défaut: `aria2`.

### ftp
((File transfer protocol))

La commande `ftp` est un protocole de communication destiné à l'échange de fichiers sur un réseau TCP/IP. Elle permet, depuis un ordinateur, de copier des fichiers vers un autre ordinateur du réseau, ou encore de supprimer ou de modifier des fichiers sur l'ordinateur distant. Ce mécanisme de copie est souvent utilisé pour alimenter un site web hébergé chez un tiers. Reportez-vous au chapitre qui lui est consacré pour plus d'informations.

``` bash
ftp adresse-ip
```

### hostname
((Host name))

Affiche ou enregistre le nom de la machine.

``` bash
hostname
```

### ifconfig
((Interface configuration))

Equivalent de `ipconfig` sous Windows, permet d'afficher et de configurer les informations des interfaces réseau installées sur la machine. Lisez attentivement le *manuel*, beaucoup d'options sont disponibles.

``` bash
ifconfig
```

### netstat

Affiche les connexions réseau, les tables de routage, les statistiques des interfaces, les connexions masquées, les messages netlink et les membres multicast.

``` bash
netstat -rn
```

### ping

La commande `ping` est une commande extrêmement utile pour savoir si un équipement (ordinateur, DNS ou site Web) est joignable via un réseau IP en calculant le temps mis pour recevoir une réponse (temps de trajet de la trame allé et retour). Elle permet aussi de déterminer le taux de paquet perdu moyen.

Elle est très utile pour débuter une investigation sur un équipement qui ne répond pas ou sur l'origine de paquets perdus ou de temps de réponses trop variables ou anormalement longs (réseau congestionné ou mauvaise qualité du câblage, etc.). Il faut passer en paramètre l'adresse IP que l'on veut joindre :

``` bash
ping 192.168.1.42
```

Il est possible, dans le cas d'un site Internet, d'utiliser directement son adresse web :

``` bash
ping www.google.com
```

Voici les principales options :

| Option 		| Signification	| Détail 																		|
| :------------	| :------------	| :----------------------------------------------------------------------------	|
| *-a*			| *audible ping*| Un son est émis à chaque réception.											|
| *-c* n		| *count*		| Arrêt de la commande quand le nombre *n* demandé est atteint.					|
| *-i*			| *interval*	| Délai entre chaque envoi.														|
| *-v*			| *verbose*		| Affiche les détails des transmissions à la fin de la commande.				|
| *-w* n		| *deadline*	| Arrêt de la commande au bout des *n* secondes indiquées.						|

### ssh
((Secure shell))

La commande `ssh` est à la fois un programme informatique et un protocole de communication sécurisé. Reportez-vous au chapitre qui lui est consacré pour plus d'informations.

``` bash
ssh -p 989 utilisateur@adresse-ip
```

### telnet
((Terminal network)) ((Telecommunication network)) ((Teletype network))

La commande `telnet` est un protocole de type client-serveur s'appuyant sur TCP. Les clients se connectent généralement sur le port 23 du serveur. Mais ce protocole n'étant pas sécurisé, `ssh` est plutôt recommandé.

``` bash
telnet adresse-ip
```

### wget

La commande `wget` permet de récupérer du contenu d'un serveur Web ou FTP.

``` bash
wget http://adresse-web
```

Voici les principales options :

| Option 			| Signification		| Détail 																						|
| :----------------	| :----------------	| :--------------------------------------------------------------------------------------------	|
| *-i*				| *input-file*		| Récupère les adresses du fichier spécifié.													|
| *-c*				| *continue*		| Reprend un téléchargement interrompu.															|
| *-S*				| *Server-response*	| Affiche les messages envoyés par les serveurs FTP ou HTTP.									|
| *-r*				| *recursive*		| Active les téléchargements récursifs.															|
| *-l*				| *level*			| Indique la profondeur maximale du téléchargement récursif (option `r`).						|
| *-p*				| *pages-requisites*| Permet d'obtenir toutes les images (etc.) nécessaire à l'affichage complet de la page HTML.	|
| *--limit-rate*=n	| *--limit-rate*	| Limite le téléchargement selon le *n* indiqué.												|

## Divers

### bc

Calculatrice en ligne de commande. Ecrivez *quit* pour revenir à l'invite du Terminal.

``` bash
bc
```

Voici les principales options :

| Option 		| Signification	| Détail 										|
| :------------	| :------------	| :--------------------------------------------	|
| *-h*			| *help*		| Affiche l'aide.								|
| *-v*			| *version*		| Affiche la version de la commande.			|

### tee

Permet de rediriger le résultat d'une commande sur deux sorties simultanées. Dans cet exemple, le résultat de la commande `ls` sera affiché dans la sortie par défaut (généralement le Terminal) mais génèrera aussi un fichier qui sera créé pour l'occasion. L'option *a* de `tee` ajoutera le résultat à la fin du fichier et n'en créera pas de nouveau.

``` bash
ls -l | tee -a fichier
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-a* file		| *append*		| Ajoute les données de sortie à la fin du fichier indiqué.			|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

## Commandes système

### fdisk

Outil pour réaliser des opérations sur les tables de partitions des disques durs, reportez-vous au *manuel* pour plus d'informations. Les droits *admin* sont nécessaires.

``` bash
sudo fdisk -l
```

### halt

Enregistre le fait que le système va s'arrêter dans le fichier `/var/log/wtmp`, puis demande au noyau d'arrêter le système. La commande `shutdown` est ensuite appelée pour éteindre le système proprement. Les droits *admin* sont nécessaires.

``` bash
sudo halt
```

Voici les principales options :

| Option 		| Détail 															|
| :------------	| :----------------------------------------------------------------	|
| *-d*			| N'écrit pas dans le fichier `/var/log/wtmp`.						|
| *-f*			| N'appelle pas la commande `shutdown`.								|
| *-w*			| Ecrit dans le fichier `/var/log/wtmp` mais ne s'éteint pas.		|

### kill
[[Primitive du shell]]

Envoie un message pour arrêter un processus. Attention cependant, il est nécessaire d'avoir son numéro PID. L'option *9* permet de terminer le processus sans demande de confirmation.

``` bash
kill -9 423
```

Dans le cas d'une commande en tâche de fond (reportez-vous au paragraphe « Commandes en tâche de fond » du chapitre « Le Terminal »), vous pouvez utiliser le symbole pourcentage « % » suivi d'un numéro qui représente la commande à terminer :

``` bash
kill %3
```

### killall
((Kill all))

Envoie un message pour arrêter tous les processus de la commande spécifiée en paramètre.

``` bash
killall commande
```

Voici les principales options :

| Option 		| Signification	| Détail 																							|
| :------------	| :------------	| :------------------------------------------------------------------------------------------------	|
| *-I*			| *Ignore-case*	| Le nom de la commande n'est pas sensible à la casse.												|
| *-i*			| *interactive*	| Demande de confirmation pour arrêter les processus.												|
| *-l*			| *list*		| Liste tous les processus de la commande spécifiée en paramètre.									|
| *-u*			| *user*		| N'arrête que les commandes de l'utilisateur spécifié (le nom de la commande est alors optionnel).	|
| *-V*			| *Version*		| Indique la version actuellement installée sur le système.											|

### lspci
((List PCI))

Liste tous les éléments PCI du système. L'option *v* affiche des informations, *vv* retourne des informations plus détaillées et *vvv* apporte encore plus de détails.

``` bash
lspci -vvv
```

### lsusb
((List USB))

Liste tous les périphériques USB connectés à la machine.

``` bash
lsusb
```

Voici les principales options :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *-v*			| *verbose*		| Affiche des informations plus détaillées.							|
| *-t*			| *tree*		| Arbre hiérarchique, l'option *v* est inopérante dans ce cas.		|
| *-V*			| *Version*		| Indique la version actuellement installée sur le système.			|

### poweroff
((Power Off))

`halt`, `reboot` et `poweroff` sont les mêmes commandes de gestion du système, elles partagent juste des noms différents. Les droits *admin* sont nécessaires.

``` bash
sudo poweroff -f
```

### ps
((Processes))

Liste les processus en cours d'utilisation, permet d'obtenir le numéro PID pour la commande `kill` par exemple.

``` bash
ps -ejh
```

Voici les principales options :

| Option 		| Détail 											|
| :------------	| :------------------------------------------------	|
| *-ef*			| Liste tous les processus.							|
| *-ejh*		| Affiche les processus en arbre de parenté.		|
| *-U* user		| Liste les processus de l'utilisateur indiqué.		|

### reboot

Enregistre le fait que le système va s'arrêter dans le fichier `/var/log/wtmp`, puis demande au noyau de redémarrer le système. La commande `shutdown` est ensuite appelée pour redémarrer le système proprement. Les droits *admin* sont nécessaires.

``` bash
sudo reboot
```

Voici les principales options :

| Option 		| Détail 															|
| :------------	| :----------------------------------------------------------------	|
| *-d*			| N'écrit pas dans le fichier `/var/log/wtmp`.						|
| *-f*			| N'appelle pas la commande `shutdown`.								|
| *-w*			| Ecrit dans le fichier `/var/log/wtmp` mais ne redémarre pas.		|

### shutdown

Arrête le système de façon sécurisée. Tous les utilisateurs connectés sont informés que le système va s'arrêter. Les droits *admin* sont nécessaires.

``` bash
sudo shutdown -r -t 5 now
```

Voici les principales options :

| Option 		| Signification	| Détail 													|
| :------------	| :------------	| :--------------------------------------------------------	|
| *-h*			| *halt*		| Eteint la machine après `shutdown`.						|
| *-r*			| *reboot*		| Redémarre la machine après `shutdown`.					|
| *-t* n		| *time*		| Eteint la machine après le temps *n* indiqué en seconde.	|

### time
[[Mot-clé du shell]]

Permet d'obtenir le temps que met une commande pour terminer son exécution complète.

``` bash
time une-commande
```

### tload

Affiche un graphique d'activité mis à jour en temps réel. Les chiffres en haut à gauche représentent la charge moyenne du système pour la dernière, les 5 et les 15 dernières minutes. Pour revenir au Terminal, utilisez la combinaison de touches <kbd>CTRL</kbd> + <kbd>C</kbd>.

``` bash
tload
```

Voici les options disponibles :

| Option 		| Signification	| Détail 													|
| :------------	| :------------	| :--------------------------------------------------------	|
| *-s* n		| *scale*		| Permet un redimensionnement à l'échelle *n* spécifiée.	|
| *-d* n		| *delay*		| Mise à jour en *n* seconde de l'affichage.				|
| *-h*			| *help*		| Affiche l'aide.											|
| *-V*			| *Version*		| Indique la version actuellement installée sur le système.	|

### top

Affiche la liste dynamique des processus en cours d'utilisation sur le système. Utiliser la touche <kbd>q</kbd> (pour *quit*) permet de revenir à la ligne de commande du Terminal et la touche <kbd>h</kbd> (pour *help*) affiche l'aide. Reportez-vous au *manuel* pour plus d'informations.

``` bash
top
```

### uptime

Indique depuis combien de temps le système fonctionne, le nombre d'utilisateurs connectés et la charge moyenne du système pour la dernière, les 5 et les 15 dernières minutes.

``` bash
uptime
```

Voici les options disponibles :

| Option 		| Signification	| Détail 													|
| :------------	| :------------	| :--------------------------------------------------------	|
| *-h*			| *help*		| Affiche l'aide.											|
| *-V*			| *Version*		| Indique la version actuellement installée sur le système.	|

## Gérer les tâches de fond

Ce chapitre reprend les commandes vues dans le paragraphe « Commandes en tâche de fond » du chapitre « Le Terminal ».

### bg
[[Primitive du shell]] ((Background))

Déplace une tâche en arrière-plan comme si elle avait été lancée avec l'esperluète « & ».

``` bash
bg %2
```

### fg
[[Primitive du shell]] ((Foreground))

Déplace une tâche au premier plan.

``` bash
fg %2
```

### jobs
[[Primitive du shell]]

Affiche l'état des tâches.

``` bash
jobs
```

Voici les options disponibles :

| Option 		| Détail 																				|
| :------------	| :------------------------------------------------------------------------------------	|
| *-l*			| Affiche le PID en plus des autres informations.										|
| *-n*			| Affiche uniquement les processus qui ont changé d'état depuis le dernier affichage.	|
| *-p*			| Affiche uniquement les PID des commandes actuellement en tâche de fond.				|
| *-r*			| Restreint l'affichage aux tâches en cours d'exécution.								|
| *-s*			| Restreint l'affichage aux tâches stoppées.											|

## Administration du système

Les commandes qui sont détaillées ici sont uniquement réservées aux administrateurs (*root*) du système GNU/Linux. Reportez-vous au chapitre sur « Le compte Root » pour plus de détails.

### addgroup
((Add group))

Permet d'ajouter un *groupe* au système.

``` bash
sudo addgroup nom-du-groupe
```

Il est possible d'ajouter un *groupe* à un utilisateur :

``` bash
sudo addgroup utilisateur nom-du-groupe
```

### adduser
((Add user))

Permet d'ajouter un *utilisateur* au système, cette commande est la même que `addgroup`. Il vous sera demandé de renseigner plusieurs informations au sujet du nouvel *utilisateur* (téléphone, bureau, etc.) :

``` bash
sudo adduser nom-utilisateur
```

ATTENTION : quand un nouvel *utilisateur* est créé, son dossier personnel est accessible en lecture pour tout le monde.

### apt-get

L'un des gestionnaire de paquets les plus utilisés, référez-vous au chapitre consacré à cette commande pour plus de détails.

``` bash
sudo apt-get update
```

### aptitude

Plus récent que `apt-get`, `aptitude` est globalement plus puissant bien que pour une utilisation courante, les deux se valent. Un chapitre lui est aussi dédié.

``` bash
sudo aptitude update
```

### chgrp
((Change group))

Permet de modifier le groupe d'un fichier/dossier. L'option *R* (pour *Recursive*) permet d'affecter récursivement le contenu d'un dossier.

``` bash
sudo chgrp groupe fichier
```

### chmod
((Change mode))

Change les droits d'accès d'un fichier ou d'un dossier. Deux façons existent pour utiliser cette commande, la première (la plus accessible) utilisant des lettres pour modifier les droits. Par exemple, pour ajouter les droits d'écriture sur un fichier (pour tous les utilisateurs) :

``` bash
sudo chmod +w fichier
```

On peut aussi modifier les droits en fonction de chacun. Par exemple, on donne à l'utilisateur les droits de lecture, d'écriture et d'exécution. Ensuite, on attribue les droits de lecture au groupe. Quant aux autres utilisateurs et groupes, on ne modifie rien (attention, il n'y a aucun espace) :

``` bash
sudo chmod u+rwx,g+r,o= fichier
```

Globalement, on peut résumer les différentes possibilités avec le tableau suivant :

| Lettre 		| Signification	| Détail 																				|
| :------------	| :------------	| :------------------------------------------------------------------------------------	|
| *a*			| *all*			| Affecte les droits à tout le monde (comportement par défaut).							|
| *u*			| *user*		| Affecte les droits à l'utilisateur du fichier.										|
| *g*			| *group*		| Affecte les droits au groupe du fichier.												|
| *o*			| *other*		| Affecte les droits aux *autres* utilisateurs du fichier.								|
| *+*			| *add*			| Ajoute des droits.																	|
| *-*			| *del*			| Supprime des droits.																	|
| *=*			| *equal*		| Ne change rien.																		|
| *x*			| *execution*	| Concerne les droits d'exécution.														|
| *X*			| *eXecution*	| Voir plus bas : « Précisions sur le drapeau X ».										|
| *r*			| *read*		| Concerne les droits de lecture.														|
| *w*			| *write*		| Concerne les droits d'écriture.														|

La deuxième méthode (le résultat est de toute façon identique), utilise le système octal. Chaque « groupement » de droits (*user*, *group* et *other*) sera représenté par un chiffre et à chaque droit correspond une valeur :

| Droit 	| Octal 	|
| :--------	| :--------	|
| *r*		| 4			|
| *w*		| 2			|
| *x*		| 1			|
| *-*		| 0			|

On ajoute les valeurs en fonction des droits que l'on veut attribuer :

| Droit 	| Valeur 	| Binaire	|
| :--------	| :--------	| :--------	|
| *rwx*		| 4+2+1 = 7	| 111		|
| *rw-*		| 4+2+0 = 6	| 110		|
| *r-x*		| 4+0+1 = 5	| 101		|
| *r--*		| 4+0+0 = 4	| 100		|
| *-wx*		| 0+2+1 = 3	| 011		|
| *-w-*		| 0+2+0 = 2	| 010		|
| *--x*		| 0+0+1 = 1	| 001		|
| *---*		| 0+0+0 = 0 | 000		|

Il est à noté que le système octal fonctionne de la façon suivante : une lettre correspond à 1 et un tiret à 0 de façon à former un nombre en binaire sur 3 bits. La conversion de ce nombre en système décimal (base 10) donne la valeur cherchée. Ainsi, `rw-` donne le nombre binaire 110 qui est égal à 6 en décimal.

Cette commande :

``` bash
sudo chmod 750 fichier
```

Produira les droits suivants : `rwxr-x---`.

Les différentes options possibles sont :

| Lettre 		| Signification	| Détail 																				|
| :------------	| :------------	| :------------------------------------------------------------------------------------	|
| *c*			| *changes*		| Similaire à l'option *verbose* mais uniquement quand il y a des changements effectués.|
| *f*			| 				| Supprime la plupart des messages d'erreur de l'affichage du Terminal.					|
| *v*			| *verbose*		| Affiche un retour de chaque fichier traité par la commande, qu’il soit modifié ou non.|
| *R*			| *Recursive*	| Applique les changements de manière récursive.										|
| *--help*		| *help*		| Affiche l'aide de la commande.														|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.								|

#### Précisions sur le drapeau X

Les dossiers doivent obligatoirement avoir la permission `x` pour pouvoir être ouverts. Pour les fichiers, cette permission n’est utile qu’aux exécutables. En outre, elle peut être gênante pour les fichiers textes (txt, html, etc.) car, à chaque ouverture, un message demandant si on veut ouvrir ou lancer le fichier s’affichera. Ce droit est donc à réserver aux seuls fichiers qui sont vraiment des exécutables (scripts ou binaires).

Partant de là, si l'on souhaite lancer une exécution de cette commande sur un dossier de manière récursive, il est nécessaire d'être vigilant quant à la modification des droits sur le drapeau `x`, aussi bien à l'ajout qu'à la suppression de celui-ci.

Par exemple, prenons le dossier « monrep », contenant des sous-dossiers et des fichiers avec les droits suivants : `drwx——----` (700) pour les dossiers et `-rw—------` (600) pour les fichiers. Maintenant, on souhaite ajouter récursivement les mêmes droits (respectivement `rwx` et `rw`) pour le groupe, c'est à dire que l'on veut aboutir à la situation suivante : `drwxrwx---` (770) pour les dossiers et `-rw-rw—---` (660) pour les fichiers. Voici ce que l'on obtiendrait avec les commandes suivantes :

- `chmod -R 770 monrep` : tous les fichiers auront les droits d'exécution ; ceci n'est pas souhaitable.
- `chmod -R 660 monrep` : les dossiers n'auront plus les droits d'exécution ; c’est catastrophique car on ne pourra plus les ouvrir.
- `chmod -R g+rwx monrep` : tous les fichiers vont avoir les droits d'exécution, le résultat est donc identique au premier exemple.
- `chmod -R g+rwX monrep` : seuls les dossiers (et les fichiers déjà exécutables) auront les droits d'exécution.

La dernière solution est celle à retenir, le `X` prend tout son sens.

Un autre exemple : imaginons qu’on ait précédemment lancé la commande `chmod -R 770 monrep`. La situation est donc la suivante : les droits sont `drwxrwx---` (770) pour les dossiers et `-rwxrwx---` (770) pour les fichiers. On souhaite supprimer les droits d'exécution uniquement sur les fichiers, c'est-à-dire que l'on veut aboutir à la situation suivante : `drwxrwx---` (770) pour les dossiers et `-rw-rw----` (660) pour les fichiers. Comme `chmod` s'applique à la fois aux fichiers et aux dossiers, nous allons jongler avec `x` et `X`. Il faut donc enlever `x` puis ajouter `X`.

Si on lance `chmod -R u-x+X,g-x+X monrep` cela n'aura aucun effet car *X* concerne à la fois les dossiers et les fichiers qui ont un drapeau `x` quelque part. Donc si *u-x* enlève le premier *x* (ce qui donne `-rw-rwx---`), la suite `+X` va aussitôt remettre un `x` car il reste le drapeau `x` du groupe.

Donc il faut d'abord enlever tous les `x` : `u-x,g-x` avant de les remettre avec `u+X,g+X` (seuls les dossiers seront affectés) ce qui donnera au final : `chmod -R u-x,g-x,u+X,g+X monrep`.

### chown
((Change owner))

Transfère le fichier ou dossier à un autre propriétaire, peut être récursif avec l'option *R* (pour *Recursive*).

``` bash
sudo chown nouveau-utilisateur fichier
```

Permet de changer, en une seule ligne, le propriétaire et le groupe :

``` bash
sudo chown nouveau-utilisateur:nouveau-groupe fichier
```

Ou uniquement le groupe :

``` bash
sudo chown :nouveau-groupe fichier
```

### cron

`cron` est un processus qui permet d'automatiser des tâches à un moment précis et de manière répétée. La méthode la plus simple est de copier (ou déplacer) le script possédant les droits d'exécution dans un des dossiers qui sont utilisés par cette commande.

| Dossier					| Exécution à				|
| :------------------------	| :------------------------ |
| `/etc/cron.hourly/`		| Chaque heure.				|
| `/etc/cron.daily/`		| Chaque jour.				|
| `/etc/cron.weekly/`		| Chaque semaine.			|
| `/etc/cron.monthly/`		| Chaque mois.				|

`cron` est en réalité constitué d'un démon : `crond`, c'est-à-dire un programme qui réside en mémoire et lance automatiquement des tâches en fonction de la table `cron`. Une commande : `crontab`, permet d'éditer la table des tâches à ordonnancer.

### crontab

Est la commande qui permet de lire et modifier le fichier *crontab*.

| Option 		| Signification	| Détail 																					|
| :------------	| :------------	| :----------------------------------------------------------------------------------------	|
| *-e*			| *editor*		| Ouvre le fichier pour appliquer les modifications directement.							|
| *-l*			| *list*		| Affiche les tâches programmées.															|
| *-r*			| *removed*		| Supprime toutes les tâches programmées, immédiatement et sans demande de confirmation.	|

#### Syntaxe de l'éditeur

L'option *e* a pour effet de lancer l'éditeur `vi` présentant la table actuelle (vide si il s'agit du premier lancement). Chaque ligne correspond à une tâche qu'il faut exécuter. La notation est la suivante :

``` bash
mm hh jj MMM JJJ commande > log
```

Concernant la syntaxe :

- `mm`			: représente les minutes (de 0 à 59)
- `hh`			: représente l'heure (de 0 à 23)
- `jj`			: représente le numéro du jour du mois (de 1 à 31)
- `MMM`			: représente le numéro du mois (de 1 à 12) ou l'abréviation du nom (jan, feb, mar, apr, ...)
- `JJJ`			: représente l'abréviation du nom du jour ou le chiffre correspondant au jour de la semaine (0 pour dimanche, 1 pour lundi, ...)
- `commande`	: représente la commande ou le script `shell` à exécuter (chemin absolu ou relatif)
- `log`			: représente le nom d'un fichier dans lequel stocker le journal des opérations. Si la clause de redirection n'est pas spécifiée, `cron` envoie automatiquement un mail de confirmation. Pour éviter ces deux comportements, il suffit de spécifier `> /dev/null`.

Pour chaque unité de temps (minute/heure/...) les notations suivantes sont possibles :

- \*	: à chaque unité de temps
- 2-5	: les unités de temps de 2 à 5
- */3	: toutes les 3 unités de temps (0,3,6,...)
- 5,8	: les unités de temps 5 et 8

#### Quelques exemples

Tous les jours à 23h30 :

``` bash
30 23 * * * df >>/tmp/log_df.txt
```

Tous les premiers du mois à 23h30 :

``` bash
30 23 1 * * df >>/tmp/log_df.txt
```

Tous les lundis à 22h28 :

``` bash
28 22 * * 1 df >>/tmp/log_df.txt
```

Du 2 au 5 de chaque mois à 10h12

``` bash
12 10 2-5 * * df >>/tmp/log_df.txt
```

Tous les jours pairs du mois à 23h59

``` bash
59 23 */2 * * df >>/tmp/log_df.txt
```

Il est également possible d'exécuter automatiquement des commandes plus complexes à l'aide d'un script `shell`. Pour ce faire, il suffit de créer un script, puis de le déclarer en tant que tâche dans la *crontab*.

### delgroup
((Delete group))

Supprime un *groupe* du système.

``` bash
sudo delgroup groupe
```

### deluser
((Delete user))

Supprime un *utilisateur* du système. Pour supprimer son dossier *home*, utilisez l'option `--remove-home` ou option `--remove-all-files` pour supprimer tous les fichiers du système possédés par l'utilisateur (l'option `--remove-home` n'a, dans ce cas, plus aucun effet).

``` bash
sudo deluser utilisateur
```

### groupadd
((Group add))

Globalement, même chose que `addgroup` mais avec des options différentes. Cette commande n'est pas disponible dans toutes les distributions GNU/Linux (Debian fait appel à `addgroup` par exemple).

``` bash
sudo groupadd nom-du-groupe
```

### groupdel
((Group delete))

Globalement, même chose que `delgroup` mais avec des options différentes. Cette commande n'est pas disponible dans toutes les distributions GNU/Linux (Debian fait appel à `delgroup` par exemple).

``` bash
sudo groupdel nom-du-groupe
```

### mount

Sur la plupart des OS modernes, une clé USB ou un disque dur externe sont automatiquement reconnus et ajoutés au système. Mais il est parfois nécessaire de les « monter » manuellement, soit pour spécifier des options de montage, soit parce que la distribution GNU/Linux que vous utilisez ne possède pas d'interface graphique. Il est alors nécessaire de passer par la ligne de commande pour ajouter un périphérique de stockage. L'opération inverse nécessite la commande `umount`.

La première étape est de regarder dans le dossier `/dev` et d'y trouver votre clé USB (`sda1` par exemple). Le montage se fait généralement dans le dossier `/media` ou encore `/mnt`. Il peut être nécessaire d'y créer des sous-dossiers afin de monter plusieurs systèmes, ce qui permettra d'organiser et de sélectionner ceux à « éjecter ».

``` bash
sudo mount /dev/sda1 /media/un-dossier
```

Pour afficher tous les montages actuellement présents sur le système ou pour vérifier que la commande utilisée précédemment s'est bien déroulé :

``` bash
mount
```

### passwd
((Password))

L'utilisateur qui souhaite changer son mot de passe utilisera directement cette commande. Un administrateur indiquera en paramètre un *utilisateur* pour réinitialiser le mot de passe de celui-ci.

``` bash
passwd -x 92 nom-utilisateur
```

Voici les principales options :

| Option 		| Signification	| Détail 																											|
| :------------	| :------------	| :----------------------------------------------------------------------------------------------------------------	|
| *-e*			| *expire*		| Le mot de passe est immédiatement désactivé. L'utilisateur, à sa prochaine connexion, devra le changer.			|
| *-h*			| *help*		| Affiche l'aide.																									|
| *-i* n		| *inactive*	| Désactive le compte après *n* jours d'inactivité si l'utilisateur ne se connecte pas pendant cette période.		|
| *-n* n		| *mindays*		| Nombre de jours minimum où le mot de passe restera valide (en *n* jours, 0 pour un changement illimité).			|
| *-x* n		| *maxdays*		| Nombre de jours maximum où le mot de passe restera valide (en *n* jours).											|
| *-S* user		| *Status*		| Affiche l'état du mot de passe pour le compte demandé, voir le *manuel* à ce sujet pour plus d'informations.		|

### rpm

Système de gestion de paquets de logiciels utilisé sur certaines distributions GNU/Linux.

### su
((Super user))

Il est fréquent que le compte **super user** soit désactivé pour des raisons de sécurité. Dans ce cas, cette commande ne sera pas fonctionnelle et un échec d'authentification vous sera renvoyé à chaque tentative. Dans le cas contraire, cette commande permet de passer **super user** sur la machine.

``` bash
su
```

Cette commande permet aussi de « devenir » un autre utilisateur, pour la durée de la session :

``` bash
su utilisateur
```

Voici les principales options :

| Option 		| Signification	| Détail 																											|
| :------------	| :------------	| :----------------------------------------------------------------------------------------------------------------	|
| *-l*			| *login*		| Fourni à l'utilisateur un environnement similaire à celui qu'il aurait obtenu s'il s'était connecté directement.	|
| *-s*			| *shell*		| Indique l'interpréteur de commande qui doit être appelé lors de la connexion.										|

### sudo
((Super user do))

Indique *admin fait*, permet « d'outrepasser » la commande `su` et d'utiliser temporairement des commandes nécessitant les accès *admin*. Actif uniquement si l'utilisateur appartient au groupe *root*.

### sudo su

Permet de passer **super user** le temps de la session. Ecrivez `exit` ou utilisez la combinaison de touches <kbd>CTRL</kbd> + <kbd>D</kbd> pour sortir et revenir à votre compte personnel. Certaines limitations, par rapport au « vrai » compte **super user**, persistent.

### umask
((User mask))

La commande `umask` (pour *masque utilisateur*) permet de définir le masque binaire déterminant les droits par défaut d'un fichier ou d'un dossier lors de sa création. Autrement dit, elle indique les droits qu'il faut retirer. Utilisée seule, elle affiche le paramètre actuel :

``` bash
umask
```

Pour modifier le masque, il faut préciser la modification en argument, en notation octale (reportez-vous à la commande `chmod` pour plus de détails) :

``` bash
umask 0022
```

La durée de vie de la commande `umask` est limitée à la session du `shell` en cours. Pour une modification permanente, il faut configurer le fichier `.profile` (cherchez la ligne concernant la commande `umask`).

Par défaut, la valeur de la commande `umask` est : 0022. La création de fichier donnera ces droits : `-rw-r--r--` ; et pour les dossiers, ces droits : `drwxr-xr-x`. Un masque de 0000 donnera les droits suivants pour un fichier : `-rw-rw-rw-` ; et ceux-là pour un dossier : `drwxrwxrwx`.

### umount

Un système de fichier « monté » avec la commande `mount` sera éjecté avec cette commande.

``` bash
sudo umount /media/un-dossier
```

### usermod
((User mode))

Modifie les caractéristiques d'un utilisateur.

``` bash
usermod utilisateur
```

Voici les principales options :

| Option 		| Signification	| Détail 																																|
| :------------	| :------------	| :------------------------------------------------------------------------------------------------------------------------------------	|
| *-a*			| *append*		| Ajoute l'utilisateur au groupe indiqué en addition aux groupes secondaires, uniquement utilisable avec l'option *G*.					|
| *-l*			| *login*		| Renomme l'utilisateur, son dossier *home* sera inchangé.																				|
| *-d*			| *home*		| Indique le nouveau dossier personnel de l'utilisateur.																				|
| *-m*			| *move-home*	| Lié à l'option *d*. Déplace les données du dossier personnel actuel vers le nouveau. Ce dernier sera créé s'il n'existe pas.			|
| *-g*			| *group*		| Change le groupe initial de l'utilisateur.																							|
| *-G*			| *Groups*		| Ajoute l'utilisateur à un nouveau groupe, il est nécessaire de rappeler l'ensemble des groupes secondaires auxquels il appartient.	|

N'hésitez pas à lire le *manuel* de cette commande, les options sont un peu trop compliquées pour qu'elles puissent être détaillées ici.

### yum
((Yellowdog updater modified))

Un autre gestionnaire de paquet. Il s'agit d'une surcouche de `rpm` gérant les téléchargements et les dépendances.

## Programmation

Ces options étant spécifiques à la programmation, reportez-vous aux *manuels* de chaque commande pour plus de détails sur leur utilisation.

### basename
((Base name))

Affiche le chemin (fichier ou dossier) demandé sans le préfixer de son arborescence.

``` bash
basename /home/user/fichier.txt
```

Retournera :

``` bash
fichier.txt
```

Pour ne pas tenir compte de son extension, ajoutez un paramètre qui détermine l'extension attendu :

``` bash
basename /home/user/fichier.txt .txt
```

Retournera :

``` bash
fichier
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### dirname
((Dir name))

Affiche le dossier parent qui contient le chemin (fichier ou dossier) demandé en paramètre de la commande.

``` bash
dirname /usr/bin/
```

Retournera :

``` bash
/usr
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### echo
[[Primitive du shell]]

Cette commande permet d'afficher une chaîne de caractères. Il n'y a pas grand intérêt à l'utiliser dans un Terminal mais elle prend tout son sens dans l'écriture de scripts. Reportez-vous à ce chapitre pour plus de détails.

``` bash
echo "Chaîne de caractères."
```

Une autre utilisation de celle-ci est de vérifier le statut de la dernière commande exécutée. 0 sera renvoyé si l'opération se déroule correctement ; tout autre chiffre indique un problème lors du traitement. Ce test est particulièrement utile lors de l'écriture de scripts.

``` bash
echo $?
```

### gcc
((GNU compiler collection))

Commande pour compiler un programme.

``` bash
gcc fichier-source -o fichier-binaire
```

### groff

Commande permettant de créer des pages de *manuel*.

### indent

Permet d'indenter les fichiers sources écrits en C, reportez-vous au *manuel* pour plus de détails.

### logger

Personnalisez les fichiers *log* générés par vos scripts.

### sleep

Marque une pause pour le temps demandé :

``` bash
sleep 6
```

Par défaut, le paramètre passé en argument est exprimé en seconde. Pour utiliser une autre unité de temps, utilisez un des suffixes suivants :

- *s*	: valeur par défaut, temps exprimé en secondes (pour *seconds*).
- *m*	: temps exprimé en minutes (pour *minutes*).
- *h*	: temps exprimé en heures (pour *hours*).
- *d*	: temps exprimé en jours (pour *days*).

Un exemple :

``` bash
sleep 1h
```

Voici les options disponibles :

| Option 		| Signification	| Détail 															|
| :------------	| :------------	| :----------------------------------------------------------------	|
| *--help*		| *help*		| Affiche l'aide de la commande.									|
| *--version*	| *version*		| Indique la version actuellement installée sur le système.			|

### source
[[Primitive du shell]]

Exécute des commandes depuis un fichier dans le Terminal.

``` bash
source fichier
```

Cette commande peut être utilisée pour recharger un fichier tel que le `.bashrc` après l'avoir modifié. Ceci permet d'éviter de relancer le Terminal ou la session.

``` bash
source .bashrc
```

Pas d'option pour cette commande.
