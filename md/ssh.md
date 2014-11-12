
# ssh

## Se connecter

La commande `ssh` permet de se connecter à un poste distant et de manière sécurisée. Pour plus d'informations : [Wikipedia](http://fr.wikipedia.org/wiki/Secure_Shell "Wikipedia : ssh").

Pour se connecter à un serveur distant, il suffit d'écrire la commande suivante :

``` bash
ssh login@adresse-ip
```

Pour se retrouver dans un dossier précis lors de la connexion :

``` bash
ssh login@adresse-ip:/dossier-de-destination
```

## Sécuriser la connexion SSH

Il est très largement déconseillé de laisser un accès `ssh` que vous auriez activé sur votre système sans appliquer quelques modifications élémentaires. Pour ce faire, éditez le fichier de configuration suivant :

``` bash
sudo vim /etc/ssh/sshd_config
```

Il vous faudra changer le port (910, par exemple) afin d’éviter les attaques automatiques sur le port 22 (port par défaut). Il faut privilégier un port inférieur ou égal à 1024 afin d'empêcher les tentatives d'usurpation par des services non administrateurs. Si la ligne *AllowUsers* n'existe pas, vous pouvez l'ajouter pour limiter uniquement certains utilisateurs à se connecter sur votre système. Si vous souhaitez autoriser plusieurs utilisateurs, séparez chaque login par des espaces. L'adresse IP peut être précisée pour augmenter un peu plus la sécurité, comme dans cet exemple : `user@192.168.1.68`. Il vous faudra aussi penser à désactiver le login *root* pour éviter la connexion d'un intrus au système qui pourrait récupérer les droits *root*. Enfin, il faut s'assurer que le protocole est en version 2. Le début du fichier doit ressembler à ceci :

``` bash
# Package generated configuration file
# See the sshd_config(5) manpage for details

# What ports, IPs and protocols we listen for
Port 910
# Use these options to restrict which interfaces/protocols sshd will bind to
#ListenAddress ::
#ListenAddress 0.0.0.0
Protocol 2
AllowUsers login
# HostKeys for protocol version 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
#Privilege Separation is turned on for security
UsePrivilegeSeparation yes

# Lifetime and size of ephemeral version 1 server key
KeyRegenerationInterval 3600
ServerKeyBits 768

# Logging
SyslogFacility AUTH
LogLevel INFO

# Authentication:
LoginGraceTime 120
PermitRootLogin no
StrictModes yes
```

Pour empêcher que les utilisateurs qui se connectent changent les variables d'environnement, paramétrez cette ligne :

``` bash
PermitUserEnvironment no
```

Enregistrez les modifications, sortez de l'éditeur de texte et redémarrez le service `ssh` avec la commande suivante :

``` bash
sudo /etc/init.d/ssh restart
```

ou

``` bash
sudo service ssh restart
```

Le port de connexion étant modifié, il faudra désormais utiliser l'option *p* (pour *port*) afin d'indiquer son numéro :

``` bash
ssh -p 910 login@adresse-ip
```

Dans tous les cas, l'usage du mot de passe est à proscrire. Reportez-vous au chapitre sur l’authentification par clés pour plus d’informations.

## Autres paramètres

Pour accéder à toutes les informations sur le fichier de configuration `sshd_config`, vous pouvez entrer la commande suivante :

``` bash
man sshd_config
```

### AllowGroups

Cette option peut être suivie d'une liste de motifs de noms de groupes, séparés par des espaces. Si un motif est spécifié, seuls les utilisateurs dont le groupe principal ou les groupes supplémentaires correspondent à ce motif sont autorisés à se connecter. On peut utiliser les caractères « \* » ou « ? » comme jokers. Seuls les noms de groupes sont valides ; les identifiants de groupes (GID) ne sont pas reconnus. Par défaut, la connexion est autorisée pour tous les groupes. Les directives *allow*/*deny* sont évaluées dans cet ordre : DenyUsers, AllowUsers, DenyGroups et AllowGroups.

### AllowTcpForwarding

Spécifie si les redirections TCP sont autorisées. Par défaut cette option est à « yes ». Il est à noter que la désactivation des redirections TCP n'améliore pas la sécurité si les utilisateurs ont un accès à un interpréteur de commandes (`shell`) car ils peuvent toujours installer leurs propres outils de redirections.

### AllowUsers

Ce mot-clef peut être suivi d'une liste de motifs de noms d'utilisateurs, séparés par des espaces. Si un motif est spécifié, seuls les noms d'utilisateurs correspondant à ce motif sont autorisés à se connecter. On peut utiliser les caractères « \* » ou « ? » comme jokers. Seuls les noms d'utilisateurs sont valides ; les identifiants d'utilisateurs (UID) ne sont pas reconnus. Par défaut, la connexion est autorisée pour tous les utilisateurs. Si le motif est de la forme `login@adresse-ip`, alors `login` et `adresse-ip` sont vérifiés séparément, en restreignant les connexions à des utilisateurs particuliers sur des machines particulières. Les directives *allow*/*deny* sont évaluées dans cet ordre : DenyUsers, AllowUsers, DenyGroups et AllowGroups.

### DenyGroups

Cette option peut être suivie d'une liste de motifs de noms de groupes, séparés par des espaces. Les utilisateurs dont le groupe principal ou les groupes secondaires correspondent à un des motifs ne sont pas autorisés à se connecter. On peut utiliser les caractères « \* » ou « ? » comme jokers. Seuls les noms de groupes sont valides ; les identifiants de groupes (GID) ne sont pas reconnus. Par défaut, la connexion est autorisée pour tous les groupes. Les directives *allow*/*deny* sont évaluées dans cet ordre : DenyUsers, AllowUsers, DenyGroups et AllowGroups.

### DenyUsers

Ce mot-clef peut être suivi d'une liste de motifs de noms d'utilisateurs, séparés par des espaces. Les utilisateurs dont le nom correspond à un des motifs ne sont pas autorisés à se connecter. On peut utiliser les caractères « \* » ou « ? » comme jokers. Seuls les noms d'utilisateurs sont valides ; les identifiants d'utilisateurs (UID) ne sont pas reconnus. Par défaut, la connexion est autorisée pour tous les utilisateurs. Si le motif est de la forme `login@adresse-ip`, alors `login` et `adresse-ip` sont vérifiés séparément, en restreignant les connexions à des utilisateurs particuliers sur des machines particulières. Les directives *allow*/*deny* sont évaluées dans cet ordre : DenyUsers, AllowUsers, DenyGroups et AllowGroups.

### PasswordAuthentication

Spécifie si l'authentification par mot de passe est autorisée. Par défaut, elle l’est : « yes ».

### PermitEmptyPasswords

Quand l'authentification par mot de passe est autorisée, cette option indique si le serveur autorise les connexions à des comptes dont les mots de passe sont des chaînes de caractères vides. Par défaut : « no ».

### PermitRootLogin

Cette option indique si le compte `root` peut se connecter via `ssh`. Le paramètre doit être réglé à : « yes », « without-password », « forced-commands-only » ou « no ». Par défaut, cette option est à « yes ». Si elle est réglée à « without-password », l'authentification par mot de passe est désactivée pour `root`. Il est très fortement recommandé de ne jamais faire ce choix, en aucun cas. Réglée à « forced-commands-only », les connexions de `root` sont autorisées avec une authentification par clef publique, mais seulement si l'option `command` est spécifiée (ce qui peut être utile pour effectuer des sauvegardes à distance même si les connexions de `root` sont normalement interdites). Toutes les autres méthodes d'authentification sont désactivées pour `root`. Paramétrée à « no », `root` n'est pas autorisé à se connecter.

### PrintLastLog

Indique si `sshd` doit afficher la date et l'heure de la dernière connexion de l'utilisateur. Par défaut cette option est à « yes ».

### PrintMotd

Indique si `sshd` doit afficher le contenu du fichier `/etc/motd` quand un utilisateur se connecte en mode interactif. Sur certains systèmes, il est aussi affiché par l'interpréteur de commandes `shell` paramétré par le fichier `/etc/profile` ou équivalent. Par défaut, cette option est à « yes ».

### Protocol

Spécifie les versions du protocole que le démon `sshd` doit gérer. Les valeurs possibles sont « 1 » et « 2 ». Pour spécifier plusieurs versions, il suffit de les séparer par des virgules. Il est à noter, dans ce cas, que l'ordre indiqué n'a aucune influence. Autrement dit, déclarer « 1,2 » ou « 2,1 » revient strictement au même. Par défaut, ce paramètre est à « 2 ».

### PubkeyAuthentication

Spécifie si on autorise l'authentification par clef publique. Par défaut, l’option est paramétrée à « yes ». Il est à noter que cette option ne s'applique qu'à la version 2 du protocole.

### StrictModes

Indique si `sshd` doit vérifier les modes et le propriétaire des fichiers de l'utilisateur et du répertoire de base (*home*) de l'utilisateur avant d'accepter une connexion. C'est normalement souhaitable car, parfois, les novices ont tendances à laisser accidentellement leur répertoire ou leurs fichiers en accès complet à tout le monde. Par défaut : « yes ».

### X11Forwarding

Spécifie si on autorise les redirections X11. Doit être paramétré à « yes » ou à « no ». Par défaut, cette option est à « no ». Il est à noter que la désactivation des redirections X11 n'améliore en aucun cas la sécurité car les utilisateurs peuvent installer leurs propres redirecteurs. La redirection X11 est automatiquement désactivée si l'option `UseLogin` est activée.

## Connexion par clés

Pour plus de sécurité sur votre connexion à distance, il vaut mieux laisser tomber la combinaison login/mot de passe et préférer la cryptographie asymétrique. Ce sujet étant relativement complexe à aborder ici et ne concernant que les aspects de sécurités informatiques, il ne sera pas traité. Vous pourrez trouver plus d'informations [ici](http://fr.wikipedia.org/wiki/Cryptographie_asym%C3%A9trique "Wikipedia : cryptographie asymétrique").

Selon la configuration `ssh` par défaut, vous pouvez vous connecter sans avoir à générer la paire de clés. Vous pouvez essayer de vous connecter directement avec cette commande :

``` bash
ssh -p 910 login@adresse-ip
```

Si vous obtenez quelque chose de similaire à ceci :

``` bash
The authenticity of host '[adresse-ip]:910 ([adresse-ip]:910)' can't be established.
RSA key fingerprint is a9:6c:14:23:d8:f4:9c:d6:73:1f:2d:cd:12:5a:b3:a1.
Are you sure you want to continue connecting (yes/no)?
```

Vous pouvez alors entrer le mot « yes » et après validation, vous serez déconnecté et un message similaire à celui-ci devrait s'afficher :

``` bash
Warning: Permanently added '[adresse-ip]:910' (RSA) to the list of known hosts.
Connection closed by adresse_ip
```

Si vous essayez à nouveau la commande suivante :

``` bash
ssh -p 910 login@adresse-ip
```

Vous serez, cette fois, connecté sur la machine distante et vous ne devriez plus revoir les messages ci-dessus avant longtemps. Cette manipulation crée le fichier `known_hosts` dans le dossier `.ssh/` de votre dossier *home*. Une suppression de ce fichier réinitialisera toute cette procédure.

Si la configuration ne vous permet pas d’effectuer les étapes vues précédemment, suivez les explications suivantes : 

### Création d'une paire de clés

Pour générer une paire de clés publique/privée, utilisez la commande suivante :

``` bash
ssh-keygen -t rsa -b 2048
```

L'option *t* (pour *type*) vous permet de sélectionner l'algorithme d'encryption. Trois choix sont possibles : *rsa*, *dsa* ou *ecdsa*. L'option *b* (pour *bits*) permet de spécifier le nombre de bits pour l'encodage. La valeur par défaut du *rsa* est de 2048 alors qu'elle est de 1024 pour le *dsa*. L'option *v* (pour *verbose*) vous donnera plus d'informations lors de la création des clés.

Le programme demandera de confirmer le dossier de destination pour générer les clés. Vous pouvez appuyer sur la touche <kbd>ENTRÉE</kbd> et laisser par défaut. Il sera alors créé, dans votre dossier *home*, un dossier caché `.ssh/` ainsi que deux fichiers `id_rsa` (la clé privée) et `id_rsa.pub` (la clé publique). Il vous sera ensuite demandé une passphrase. N'hésitez pas à écrire une phrase longue avec des minuscules, des majuscules ainsi que des chiffres et des caractères spéciaux. Une fois cette opération effectuée, modifiez les droits des clés avec la commande suivante (par mesure de précaution) :

``` bash
chmod 600 .ssh/id*
```

Ceci étant fait, il faudra copier, de manière sécurisée, la clé publique sur la machine distante. Si votre configuration client/serveur se trouve sur le même réseau local, ne prenez pas de précautions trop contraignantes, elles seraient inutiles. Vous pouvez effectuer le transfert avec une simple clé USB. La clé publique ainsi créée sur la machine locale pourra être renommée, déplacée ou supprimée.

Une autre possibilité pour copier la clé sur la machine distante :

``` bash
ssh login@adresse-ip "echo $(cat ~/.ssh/id_dsa.pub) >> .ssh/authorized_keys"
```

Maintenant que les clés sont créées et que vous avez copié la clé publique, il est nécessaire de paramétrer cette option dans le fichier `sshd_config` :

``` bash
PasswordAuthentication no
```

Ainsi que celle-ci :

``` bash
UsePAM no
```

Et de vérifier que cette option ne soit pas à « no » :

``` bash
PubkeyAuthentication yes
```

Enfin, il est impératif d'indiquer l'endroit où se trouve la clé publique que vous avez copié précédemment (le nom de ce fichier peut être modifié si plusieurs clés doivent y être stockées) :

``` bash
AuthorizedKeysFile .ssh/id_rsa.pub
```

Redémarrez ensuite `ssh` :

``` bash
sudo service ssh restart
```

Désormais, lors de la prochaine connexion, le mot de passe vous sera demandé (la passphrase entrée plus haut) et vous serez connecté sur la machine distante.

## Configurer le motd

Abréviation de *Message Of The Day*, le contenu de ce fichier peut être affiché à la connexion de l'utilisateur. Cela peut être un message de bienvenue ou du ASCII Art par exemple. On peut aussi, par l'intermédiaire d'un cron, générer automatiquement un fichier avec certaines informations telles que la date, l'heure, la température du processeur, etc. Attention, ce fichier ne doit pas dépasser 64ko. Pour le personnaliser, il suffit d'éditer ce fichier avec la commande suivante :

``` bash
sudo vim /etc/motd
```

Il peut être nécessaire de configurer cette ligne dans le fichier `sshd_config` :

``` bash
PrintMotd yes
```

## scp

A présent que le tunnel `ssh` est configuré et fonctionnel, la commande `scp` peut être mise à contribution. Pour copier un fichier de manière sécurisée entre deux machines :

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
