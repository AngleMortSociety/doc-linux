
# Scripting

## Principes de base

ATTENTION : les espaces dans les exemples de codes qui suivent sont très importants. Un espace en trop ou en moins peut, dans certains cas, rendre le script non fonctionnel et renvoyer des erreurs à l'exécution.

Un script commence toujours avec le *Sha-Bang* :

``` bash
#!/bin/bash
```

`bash` n'est pas le seul *shell* : vous pouvez le remplacer notamment par `sh` ou `ksh`.

Utilisez des extensions de fichiers pour vos scripts en relation avec le `shell` que vous avez choisi lors de l'écriture du *Sha-Bang*. Ceci permettra d'identifier immédiatement sous quel `shell` ils sont écrits : `exemple.bash` ou `exemple.ksh`.

Un fichier contenant un script doit posséder les droits d'exécution de l'utilisateur qui compte s'en servir pour que celui-ci fonctionne.

## Les commentaires

Pour commenter une instruction et ainsi la rendre inactive à l'exécution ou tout simplement pour annoter votre travail, utilisez une dièse « # », en début de ligne :

``` bash
# Un commentaire
```

## Les conditions

Voici un bloc conditionnel complet :

``` bash
if [ test ]
then
	echo "Le premier test a été vérifié"
elif [ autre_test ]
then
	echo "Le second test a été vérifié"
elif [ encore_autre_test ]
then
	echo "Le troisième test a été vérifié"
else
	echo "Aucun des tests précédents n'a été vérifié"
fi
```

### Tests sur des chaînes de caractères

| Condition					| Signification																										|
| :------------------------ | :---------------------------------------------------------------------------------------------------------------- |
| -n Chaîne1				| La longueur de la Chaîne1 n'est pas nulle.																		|
| -z Chaîne1				| La longueur de la Chaîne1 est nulle.																				|
| Chaîne1 = Chaîne2			| Chaîne1 et Chaîne2 sont identiques. Notez que bash est sensible à la casse : « b » est donc différent de « B ».	|
| Chaîne1 != Chaîne2		| Chaîne1 et Chaîne2 sont différentes.																				|
| Chaîne1					| Chaîne1 n'est pas une chaîne de caractères nulle.																	|

Pour les habitués du langage C, il est possible d'écrire deux fois le symbole d'égalité « == » lors des tests d'équivalence.

### Tests numériques

| Condition					| Signification																					|
| :------------------------ | :-------------------------------------------------------------------------------------------- |
| $Entier1 -eq $Entier2		| Entier1 et Entier2 sont, algébriquement parlant, égaux.										|
| $Entier1 -ne $Entier2		| Entier1 n'est pas égal à Entier2.																|
| $Entier1 -gt $Entier2		| Entier1 est strictement supérieur à Entier2.													|
| $Entier1 -ge $Entier2		| Entier1 est supérieur ou égal à Entier2.														|
| $Entier1 -lt $Entier2		| Entier1 est strictement inférieur à Entier2.													|
| $Entier1 -le $Entier2		| Entier1 est inférieur ou égal à Entier2.														|

### Caractéristiques de fichiers

| Condition					| Signification																					|
| :------------------------ | :-------------------------------------------------------------------------------------------- |
| -b Fichier				| Fichier existe et est un fichier spécial en mode bloc.										|
| -c Fichier				| Fichier existe et est un fichier spécial en mode caractère.									|
| -d Fichier				| Fichier existe et est un répertoire.															|
| -e Fichier				| Fichier existe.																				|
| -f Fichier				| Fichier existe et est de type ordinaire.														|
| -g Fichier				| Fichier existe et le bit Set Group ID est actif.												|
| -h Fichier				| Fichier existe et est un lien symbolique.														|
| -k Fichier				| Fichier existe et le sticky bit est actif.													|
| -L Fichier				| Fichier existe et est un lien symbolique (même chose que -h).									|
| -p Fichier				| Fichier existe et est un tube nommé (*named pipe*, FIFO).										|
| -r Fichier				| Fichier existe et est accessible en lecture.													|
| -S Fichier				| Fichier existe et est un fichier spécial socket.												|
| -s Fichier				| Fichier existe et a une taille non nulle.														|
| -t Descripteur			| Le descripteur de fichier est ouvert et associé à un terminal.								|
| -u Fichier				| Fichier existe et le bit Set User ID est actif.												|
| -w Fichier				| Fichier existe et est spécifié comme étant accessible en écriture. Cependant, il ne sera pas accessible en écriture sur un système de fichier en lecture seule, même si le test indique vrai (*true*).												|
| -x Fichier				| Fichier existe et est spécifié comme étant exécutable. Si le fichier spécifié est un répertoire, une valeur de retour vrai (*true*) signifie que le processus courant a la permission de parcourir ce répertoire.											|

### Comparaisons au niveau des fichiers

| Condition					| Signification																												|
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| Fichier1 -nt Fichier2		| Fichier1 est plus récent que Fichier2.																					|
| Fichier1 -ot Fichier2		| Fichier1 est plus ancien que Fichier2.																					|
| Fichier1 -ef Fichier2		| Fichier1 et Fichier2 pointent vers le même fichier (par le biais d'un lien symbolique ou d'un lien physique).				|

### Opérateurs

Tous les tests ci-dessus peuvent être combinés avec les opérateurs suivants :

| Condition					| Signification																												|
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| !							| Opérateur unaire de la négation.																							|
| -a						| Opérateur binaire ET.																										|
| -o						| Opérateur binaire OU (l'opérateur *-a* est prioritaire sur l'opérateur *-o*).												|
| \(Expression\)			| Les parenthèses pour effectuer des groupements doivent être échappées par des antislashs (barre oblique inversée, « \ »).	|

### Code de retour

| Code						| Signification																												|
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------ |
| 0							| L'expression conditionnelle est vraie (*true*).																			|
| 1							| L'expression conditionnelle est fausse (*false*).																			|
| >1						| Une erreur s'est produite.																								|

Les conditions « ET » s'écrivent de la façon suivante :

``` bash
if [ $# -ge 1 ] && [ $1 = "koala" ]
```

Les conditions « OU » :

``` bash
if [ $# -ge 1 ] || [ $1 = "koala" ]
```

Il est possible d'inverser un test en utilisant la négation. En `bash`, c'est le point d'exclamation « ! » :

``` bash
if [ ! -e fichier ]
```

## Le case

``` bash
case "$1" in
	"Bruno")
		echo "Salut Bruno !"
		;;
	"Michel")
		echo "Bien le bonjour Michel"
		;;
	*)
		echo "Je ne te connais pas, au revoir !"
esac
```

## Boucles while

``` bash
while [ test ]
do
	echo 'Action en boucle'
done
```

## Boucles for

``` bash
for variable in 'valeur1' 'valeur2' 'valeur3'
do
	echo "La variable vaut $variable"
done
```

## Simuler un for classique

``` bash
for i in `seq 1 10`;
do
	echo $i
done
```

## Les variables

Pour déclarer une variable :

``` bash
maVariable="bonjour"
```

Les caractères d'échappement sont les antislashs « \ », exemple :

``` bash
maVariable="\"J'achèterai tout\", a dit l'or ; \"Je prendrai tout\", a dit l'épée. - Alexandre Pouchkine."
```

Pour utiliser le contenu d'une variable, utilisez le symbole dollar « $ » devant le nom de celle-ci, exemple :

``` bash
$maVariable
```

Pour afficher une variable, l'instruction `echo` est utilisé :

``` bash
echo $maVariable
echo Ceci est un message composé de plusieurs variables
echo "Ceci est une chaîne de caractère."
```

## Les guillemets

En fonction du résultat souhaité, il est important de choisir les guillemets avec discernement.

### Interprétation

En fonction des guillemets utilisés, certains caractères ainsi que le contenu des variables auront un résultat différent.

#### Chaîne de caractères

Pour affecter une chaîne de caractères à une variable, utilisez les guillemets doubles :

``` bash
uneChaine="Ceci est une chaîne de caractères."
```

L'utilisation de cette variable (avec la commande `echo`) affichera le contenu de celle-ci :

``` bash
echo $uneChaine

=> Ceci est une chaîne de caractères.
```

L'usage des guillemets doubles avec la commande `echo` est possible, le résultat est identique :

``` bash
echo "$uneChaine"

=> Ceci est une chaîne de caractères.
```

Le symbole dollar « $ » est interprété au sein des guillemets doubles : le contenu d'une variable est donc affiché.

#### Guillemets doubles

Quand une commande appelle une variable contenant une commande quelconque, le choix des guillemets est très important. Les guillemets doubles interprètent certains caractères. Par exemple, avec la commande `pwd` :

``` bash
uneCommande="pwd"
```

Les guillemets doubles restent une chaîne de caractères, la commande n'est pas interprétée mais la variable reste évaluée :

``` bash
echo "$uneCommande"

=> pwd.
```

Comme le signe du dollar « $ », les guillemets inverses sont aussi interprétés à l'intérieur des guillemets doubles :

``` bash
echo "Je me trouve dans le dossier : `pwd`"

=> Je me trouve dans le dossier : /home/user # Par exemple.
```

#### Guillemets simples

Les guillemets simples afficheront le nom de la variable :

``` bash
echo '$uneCommande'

=> $uneCommande.
```

Ceci montre que les guillemets simples n'interprètent pas le symbole dollar « $ », l'antislash « \ » et les quotes inverses « ` » : les variables ne sont pas évaluées.

#### Guillemets inverses

L'usage des quote inverses permet d'interpréter une commande attribuée à la variable :

``` bash
echo `$uneCommande`

=> /home/user # voir la ligne uneCommande="pwd" plus haut.
```

### Pour résumer

- les guillemets doubles « " »	: permettent l'interprétation des caractères spéciaux (« $ », « \ » et « ` »)
- les guillemets simples « ' »	: affichent le contenu tel quel, aucune interprétation n'est réalisée
- les guillemets inverses « ` »	: exécutent une commande

### Retour utilisateur

Pour demander une saisie au clavier de la part de l'utilisateur, on utilise l'instruction `read` et une variable doit être attribuée :

``` bash
read nomVariable
```

L'option *p* permet d'afficher le prompt, c'est à dire la ligne clignotante du Terminal. Une chaîne de caractère est obligatoire pour l'accompagner :

``` bash
read -p "Entrez votre nom : " maVariable
```

## Exécution de script

Pour exécuter un script, vous devez écrire le nom du fichier précédé de « ./ ». Si vous ne le faite pas, le système est incapable de lancer le script car il le cherche dans la variable d'environnement PATH. Pour éviter de rajouter ces deux symboles, vous pouvez ajouter le dossier contenant votre script à cette variable.

### Ajoutez un répertoire à la variable PATH

#### Seulement pour la session en cours

Si on veut ajouter par exemple `/home/user/mes_prog` à la variable PATH :

- `export PATH=$PATH:/home/user/mes_prog`	: Ajoutera le dossier en dernier.
- `export PATH=/home/user/mes_prog:$PATH`	: Ajoutera le dossier en premier, peut-être dangereux.

Maintenant, vous pouvez utiliser votre programme en écrivant tout simplement son nom. A la déconnexion, PATH reprendra sa valeur par défaut, `/home/user/mes_prog` n'existera plus.

#### De manière permanente

Si vous voulez configurer le PATH de manière permanente, alors vous devez éditer le fichier de configuration de votre `shell` de connexion. Comme le plus souvent c'est le shell `bash` qui est utilisé, vous devez éditer votre fichier `/home/user/.bashrc` (sur certains système, il faut regarder dans le `.profile`).

Vous pouvez aussi écrire dans le terminal :

``` bash
echo `export PATH=$PATH:/home/user/mes_prog` >> /home/user/.bashrc
```

Ainsi, à chaque connexion, votre PATH contiendra votre répertoire `/home/user/mes_prog`. Cette opération peut être exécutée par l'utilisateur *user* vu qu'il s'agit de son environnement. L'ordre dans lequel les chemins sont écrits dans le PATH est important car il détermine la priorité dans lequel le PATH doit aller chercher une commande. Quand une commande est exécutée, elle est cherchée au premier emplacement puis au suivant et ainsi de suite.

## Astuces sur les scripts

Mettre un antislash « \ » devant une commande (`find`, `bzip2`, etc.) permet d'éviter des éventuels *alias* créés par l'utilisateur. Effectivement, si un *alias* est créé et que `find` fait autre chose que la commande initiale, le script aura un comportement inattendu.

Quand on a un problème avec un script, on peut utiliser le débogueur avec l'instruction `set -x` qui doit-être placée en premier, directement après le *Sha-Bang* :

``` bash
#!/bin/bash
set -x

# La suite du script...
```

Pour vérifier qu'une commande s'est bien exécutée, écrivez la ligne suivante :

``` bash
echo $?

=> retourne 0 si aucun problème n'a été rencontré ; un autre chiffre est renvoyé dans le cas contraire.
```

Cette ligne peut être utilisée dans le `bash`, à tout moment, après l'exécution d'une commande.

Attention aux noms de dossiers avec des espaces. Pour éviter tout problème, écrivez ceci :

``` bash
MaVariableDossier="dossier/dossier avec espaces"
ls "$MaVariableDossier"
```

En exécutant la `$variable` avec des doubles-quote, elle sera interprétée (comme vue plus haut) et les espaces ne poseront pas de problème particulier.

Si vous rencontrez un problème avec un test, utilisez deux fois les crochets dans les conditions :

``` bash
if [[ ! -e fichier ]]
```

A la place des crochets, vous pouvez aussi utiliser le mot-clé `test` :

``` bash
if test ! -e fichier
```

Récupération des paramètres d'un script :

- `$0` : Nom du script.
- `$1` : Premier argument. Valable de $1 à $9.
- `$#` : Nombre d'arguments passés au script.
- `$*` : Liste de tous les arguments (sauf $0) concaténés en une chaîne unique.
- `$@` : Liste de tous les arguments (sauf $0) individuellement en chaîne unique.

Pour inclure un script dans un autre, il suffit d'utiliser la commande `source`. Elle importe un fichier à l'endroit où se trouve cette instruction. Pour prendre un exemple sur le langage C, elle a le même effet que la commande de pré-processeur `#include`.

``` bash
source fichier
```

Le point est un synonyme de la commande `source`.

``` bash
. fichier
```

## Utiliser de la couleur

Il est parfois nécessaire d'utiliser de la couleur ou certaines mises en forme (gras, italique, clignotant) dans des scripts afin d'obtenir une meilleure visualisation du résultat, notamment dans les fichiers de log. La commande de base est la suivante :

``` bash
echo -e '\033[A;B;CmUne chaine de caractère.\033[0m'
```

L'option *e* permet de prendre en compte les paramètres échappés avec les antislashs « \ ». On retrouve ensuite les valeurs A, B et C. A correspond à un effet affecté au texte affiché ; B indique une couleur de texte et enfin C indique la couleur de fond. La séquence `\033[` délimite l'entrée de ces valeurs alors que : `\033[0m` clôt ces préférences et revient aux valeurs définies par défaut du Terminal. Respectez à la lettre les « ; » et n'utilisez pas d'espaces (uniquement à l'intérieur de votre texte). Il est à noter que la séquence `\033` représente le caractère ASCII d’échappement et le caractère « m » indique une séquence d’échappement de couleur. Le `0m` final permet donc de revenir aux couleurs par défaut.

Avec la commande `printf`, le résultat est identique :

``` bash
printf '\033[A;B;CmUne chaine de caractères.\033[0m'
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

Il est possible de n'indiquer qu'une ou deux valeur sur les trois, par exemple :

``` bash
echo -e '\033[1mUne chaine de caractères\033[0m'
```

D'autres exemples :

``` bash
echo -e '\033[31mAttention :\033[0m Ceci est un message important.'
```

``` bash
echo -e '\033[7;31;30mInformation :\033[0;5m Ceci est une information.\033[0m'
```

## Exemples de scripts

Recherche (commande `find`), à partir du dossier courant, les fichiers avec la permission *s* (`-perm +s`). L'instruction `-exec` permet de lancer des commandes sur les fichiers ainsi trouvés. Avec le `chmod` qui suit, les autorisations *s* sont enlevées.

``` bash
find . -perm +s -exec \chmod g-s {}\;
```

La même chose sur tous les fichiers (grâce à l'étoile qui suit le point) :

``` bash
find . * -exec \chmod g-s {}\;
```

Un script lancé par la `crontab` tous les dimanches à midi :

``` bash
#!/bin/bash

# Création de la date au format ANNEE_mois_jour.
date=`date +%Y_%m_%d`

# Variable pour le nom du fichier.
file_master="_results_bzip2_db_master.log"

# Concaténation de la date et du nom de fichier final.log
join_master=$date$file_master
\find /data1/data2/users/ \( -iname '*.db*' -o -iname '*.master*' -o -iname '*.pch*' \) -cmin +43200 -type f -fprintf /data1/scripts/validation/crontab/log/$join_master "%u \t %CD \t %k \t %p \n" -exec \bzip2 {}\;
```

On commence par le *Sha-Bang* puis on crée, à l'exécution du script, une variable contenant la date. On choisit ensuite un nom de fichier. Ces deux variables sont ensuite assemblées pour créer un nom de fichier complet, mis à jour en fonction de la date (grâce à la variable qui contient la date). La ligne `find` va lancer une recherche dans le chemin suivant : `data1/data2/users/`. Les fichiers recherchés sont les `*.db*` `*.master*` et `*.pch*`. L'option *-iname* permet de ne pas tenir compte de la casse sur le nom des fichiers. L'option *-o* est l'opérande OU ; autrement dit, cette option cherche ce fichier OU celui-ci OU celui-là. La valeur *-cmin* détermine le temps (plus de 15 jours si on fait une conversion des minutes). Quant au *-type f*, cela signifie que le code ne prend en compte que les fichiers (f pour *file*).

Pour finir, la fonction *-fprintf* permet d'écrire le résultat dans le fichier `/data1/scripts/validation/crontab/log/$join_master` au format suivant : « %u » permet de donner le nom de l'utilisateur propriétaire du fichier, « %CD » donne le chemin, « %k », le poids du fichier et « %p », le nom du fichier. Enfin, les « \t » sont des tabulations dans le fichier texte, le « \n » permet un retour à la ligne.

## Pour aller plus loin

Le lien suivant est une traduction complète de toutes les possibilités du scripting sous les systèmes GNU/Linux : [Guide avancé d'écriture des scripts Bash][].

[Guide avancé d'écriture des scripts Bash]: http://abs.traduc.org/ "Guide avancé d'écriture des scripts Bash"
