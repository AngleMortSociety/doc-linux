
# Sécuriser son système

Ce chapitre est consacré à la sécurité de votre système GNU/Linux. Vous y trouverez des conseils pour sécuriser au maximum vos données. Toutefois, ne vous servez pas de ce document comme seule référence.

## Règle des mots de passe

Un mot de passe doit contenir au minimum entre 8 et 12 caractères. Les règles pour construire son mot de passe divergent entre les différents sites Internet. N'hésitez néanmoins pas à employer des mots de passe plus longs pour les sites sensibles, comme les banques (entre 24 et 32 caractères). Un mot de passe doit-être composé (quand cela est autorisé) :

- De lettres minuscules et majuscules (de « A » à « Z » et de « a » à « z »)
- De chiffres (de « 0 » à « 9 »)
- De caractères spéciaux (« . », « / », « _ » etc.)

Quelques conseils supplémentaires :

- Evitez les mots du dictionnaire
- Ne pas employer le nom de son chien, sa date de naissance, etc.
- Evitez les mots de passe écrits sur papier
- Multiplier les systèmes de sécurité ou le système de paire de clé publique/privée, quand cela est possible

## fail2ban

Développé en langage *Python*, [fail2ban][] est un logiciel libre permettant d'analyser des fichiers de logs et de déclencher des actions si certaines choses suspectes sont détectées. La grande force de `fail2ban` est sa grande modularité que cela soit au niveau des mécanismes de détection, basés sur les expressions régulières, ou sur les actions à mener qui peuvent aller de l'expédition d'un mail à la mise en place de règles de Firewall. Vous pouvez trouver plus d'informations sur le site [Ubuntu-fr][].

`fail2ban` se base sur un système de prisons (*jails*) que l'on peut définir, activer ou désactiver dans un simple fichier de configuration (`/etc/fail2ban/jail.conf`).

Une prison est composée, entre autres, des éléments suivants:

- Nom du fichier de log à analyser.
- Filtre à appliquer sur ce fichier de log (la liste des filtres disponibles se trouve dans le dossier `/etc/fail2ban/filter.d`). Il est bien sûr possible de créer ses propres filtres.
- Paramètres permettant de définir si une action doit être déclenchée quand le filtre correspond (*match*) : Nombre de *matchs* (*maxretry*), intervalle de temps correspondant (*findtime*), etc.
- Action à mener si nécessaire. La liste des actions se trouve dans le dossier `/etc/fail2ban/action.d`. Il est également possible de créer ses propres actions.

### Installation

Ce démon lit les logs de divers serveurs (`ssh`, `apache`, `ftp`, etc.) à la recherche d'erreurs d'authentification répétées et ajoute une règle *iptables* pour bannir l'adresse IP de la source. Tout d'abord, il faut installer le paquet :

``` bash
sudo aptitude update && aptitude install fail2ban
```

Exécutez la commande suivante pour lancer le programme :

``` bash
sudo fail2ban-client -x start
```

### Configuration de base

Il est recommandé de dupliquer le fichier `jail.conf` en `jail.local`, comme ceci :

``` bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Ensuite, d'éditer le fichier `jail.local`

``` bash
sudo vim /etc/fail2ban/jail.local
```

Et de modifier dans ce dernier les configurations de base avec les paramètres spécifiques (voir ci-dessous).

### ssh

Afin de se protéger contre les attaques *brute force* `ssh`, explorez le fichier et recherchez le bloc `ssh`, puis, apportez les modifications suivantes :

``` bash
[ssh]

enabled		= true
port		= ssh,sftp,910 # précisez uniquement le port si il est différent de 22.
filter		= sshd
logpath		= /var/log/auth.log
maxretry	= 3
```

Dans l'ordre, cela active la surveillance du protocole `ssh`, les ports à bloquer avec les règles *iptables*, le nom du filtre (expression régulière) associé, le fichier de log à lire et, pour terminer, le nombre maximal de tentatives autorisées. Un certain nombre de services disposent de tels blocs de configuration, vous pouvez les activer en passant, si besoin, la valeur de `false` à `true`. Si vous avez changé le port `ssh` par défaut (voir le chapitre concernant cette commande), précisez-le sur la ligne *port* comme indiqué ci-dessus en commentaire.

Vous pouvez ainsi activer d'autres services (comme `apache2`). Il sera alors nécessaire, à chaque modification du fichier, de relancer `fail2ban` comme ceci :

``` bash
sudo fail2ban-client reload
```

### apache

Si `apache` est installé sur votre système, vous devez ajouter une règle anti *w00tw00t* qui est un robot qui scanne le réseau à la recherche de failles. Pour ce faire, il faut ajouter dans le fichier `jail.local` les lignes ci-dessous :

``` bash
[apache-w00tw00t]

enabled		= true
filter		= apache-w00tw00t
action		= iptables[name=Apache-w00tw00t,port=80,protocol=tcp]
logpath		= /var/log/apache*/*access.log
maxretry	= 1
```

Vous devez aussi ajouter le fichier de règles `/etc/fail2ban/filter.d/apache-w00tw00t.conf` qui doit contenir ceci :

``` bash
[Definition]

failregex = ^<HOST> -.*"GET \/w00tw00t\.at\.ISC\.SANS\.DFind\:\).*".*

ignoreregex =
```

### Configuration avancée

Si vous avez ce message d'erreur quand vous lancez `fail2ban` :

``` bash
WARNING 'findtime' not defined in 'ssh'. Using default value
```

Ouvrez le fichier `jail.local` et dans la section *default*, ajoutez la ligne `findtime` suivante :

``` bash
[DEFAULT]

ignoreip	= 127.0.0.1/8
findtime	= 900
bantime		= 31556926
maxretry	= 2
```

- `findtime`	: Détermine la durée pendant laquelle les tentatives de connexions ont lieu
- `bantime`		: Détermine la durée du bannissement. Toutes ces valeurs sont en seconde
- `maxretry`	: Détermine le nombre de tentatives de connexions pendant la durée `findtime`

Pour activer le filtre *SASL* permettant le bannissement en cas d'attaque par force brute, il faut modifier l'expression régulière du filtre dans ce fichier :

``` bash
sudo vim /etc/fail2ban/filter.d/sasl.conf
```

Remplacez la ligne :

``` bash
failregex = (?i): warning: [-._\w]+\[<HOST>\]: SASL (?:LOGIN|PLAIN|(?:CRAM|DIGEST)-MD5) authentication failed(: [A-Za-z0-9+/]*={0,2})?$
```

Par :

``` bash
failregex = (?i): warning: [-._\w]+\[<HOST>\]: SASL (?:LOGIN|PLAIN|(?:CRAM|DIGEST)-MD5) authentication failed: \w
```

On teste maintenant si la règle s'applique bien avec la commande suivante :

``` bash
fail2ban-regex /var/log/mail.log /etc/fail2ban/filter.d/sasl.conf
```

### Commandes de base

Comme vu plus haut, pour démarrer `fail2ban`, entrez la commande suivante :

``` bash
sudo fail2ban-client -x start
```

Pour le relancer :

``` bash
sudo fail2ban-client reload
```

Afin de vérifier que les services sont bien actifs :

``` bash
sudo fail2ban-client status
```

Pour vérifier un service particulier, ici `ssh` :

``` bash
sudo fail2ban-client status ssh
```

Les « prisons » peuvent être contrôlées séparément avec les mots clés *start*, *stop* ou *status*.

### Se « débannir »

Il peut arriver que vous ayez besoin d'autoriser une adresse IP bloquée par `fail2ban`, après une erreur de manipulation. Dans ce cas, il faut d'abord vérifier que la machine est bien présente dans la liste des blocages. Utilisez la commande suivante :

``` bash
sudo iptables -L fail2ban-ssh
```

En retour, vous obtiendrez quelque chose comme :

``` bash
Chain fail2ban-ssh (1 references)
target  prot opt source   destination
DROP    all  --  Windows8 anywhere
RETURN  all  --  anywhere anywhere
```

Ce tableau indique des « target », « prot », « opt », « source » et « destination ». Dans la première colonne, les «target» identifiés par le terme *DROP* sont les cibles interdites. Pour « débannir » une machine qui voudrait se connecter, il faudra alors écrire cette commande dans un terminal :

``` bash
sudo iptables -D fail2ban-ssh 1
```

Le chiffre en fin de commande indique la ligne affectée du tableau précédent. Dans ce cas précis, il s'agit de « Windows8 ». Il est possible de vérifier le bon déroulement de l'opération précédente avec la commande suivante :

``` bash
sudo iptables -L fail2ban-ssh
```

Et vous aurez ceci :

``` bash
Chain fail2ban-ssh (1 references)
target  prot opt source   destination
RETURN  all  --  anywhere anywhere
```

La machine « windows8 » n'étant plus présente, elle pourra à nouveau se connecter sans difficulté.

## Aller plus loin

Pour sécuriser encore plus votre système, il est fortement conseillé de désinstaller, s'ils sont présents, les paquets suivants :

- `telnet`
- `rsh`
- `rlogin`

Attention toutefois, il est possible, en écrivant une des commandes suivantes pour localiser l'un de ces paquets : `which telnet`, `which rsh` et `which rlogin`, d'avoir ce genre de retour : `/usr/bin/telnet`, `/usr/bin/rsh` et `/usr/bin/rlogin`.

Il s'agit peut-être d'un alias, entrez alors commande suivante :

``` bash
readlink -f /usr/bin/rsh
```

Si vous avez ce retour :

``` bash
/usr/bin/ssh
```

Alors il s'agît bien d'un alias. Cela peut aussi être vérifié par la commande suivante :

``` bash
ls -l /usr/bin/rsh
```

Dans ce cas, il ne s'agît que d'un lien vers la commande `ssh` qui assure une compatibilité. Il y a quelques années, certains logiciels reposaient sur `rsh` ou `rlogin`. Aujourd'hui, grâce à ces liens, ils peuvent utiliser `ssh` sans modification.

Pour en avoir le cœur net, n'hésitez pas à écrire ceci dans votre Terminal : `sudo aptitude remove telnet`, `sudo aptitude remove rsh` et `sudo aptitude remove rlogin`.

## rootkits
	
Pour la détection de rootkits, vous pouvez utiliser [Rootkit Hunter][] (ou un équivalent tel que [chkrootkit][])

Pour *Rootkit Hunter*, vous pouvez l'installer avec la commande suivante :

``` bash
sudo aptitude install rkhunter
```

Il procédera à des détections journalières anti-rootkits et enverra des notifications par e-mail si nécessaire. Il est conseillé de l'installer très tôt car il calcule l'empreinte MD5 des programmes installés afin de détecter d'éventuels changements. Afin de paramétrer la commande, éditez le fichier suivant :

``` bash
vi /etc/default/rkhunter
```

Et indiquez l'adresse de notification :

``` bash
REPORT_EMAIL="votre@mail.com"
```

En cas de fausses détections positives sur des répertoires ou fichiers existants et sains, éditez le fichier `/etc/rkhunter.conf` pour les ajouter à la liste des éléments autorisés. Exemple :

``` bash
ALLOWHIDDENDIR=/dev/.udev
ALLOWHIDDENDIR=/dev/.static
```

### Utilisation

Afin de vérifier que vous avez la dernière version disponible :

``` bash
sudo rkhunter --versioncheck
```

Pour mettre à jour le programme :

``` bash
sudo rkhunter --update
```

Lister les différents tests effectués :

``` bash
sudo rkhunter --list
```

Pour effectuer une vérification complète de votre système :

``` bash
sudo rkhunter --checkall
```

## Services inutiles

Certains services, présents sur votre machine en fonction de votre distribution GNU/Linux et de vos choix d'installation, ne vous seront surement jamais utiles. Parmi ceux-ci, il y a par exemple `portmap`, `nfs` ou encore `inetd` (dans le cas d'un serveur web, vous n'en avez pas besoin). Ainsi, il peut être intéressant de les supprimer afin d'éviter des failles de sécurité mais aussi d'économiser de la mémoire vive. Pour ce faire, il faut d'abord stopper le service puis le supprimer : 

``` bash
sudo /etc/init.d/portmap stop
```

``` bash
sudo update-rc.d -f portmap remove
```

``` bash
sudo /etc/init.d/nfs-common stop
```

``` bash
sudo update-rc.d -f nfs-common remove
```

``` bash
sudo update-rc.d -f inetd remove
```

``` bash
sudo apt-get remove portmap
```

``` bash
sudo apt-get remove ppp
```

## Autorisations diverses

Une bonne attitude est de n'autoriser les compilateurs et les installeurs que pour l'utilisateur `root` (le numéro de version est à adapter selon la version de votre distribution GNU/Linux) :

``` bash
sudo chmod o-x /usr/bin/gcc-4.6
```

``` bash
sudo chmod o-x /usr/bin/make
```

``` bash
sudo chmod o-x /usr/bin/apt-get
```

``` bash
sudo chmod o-x /usr/bin/aptitude # /usr/bin/aptitude-curses
```

``` bash
sudo chmod o-x /usr/bin/dpkg
```

## Base de données

Si vous avez une base de données MySQL installée sur votre système, reportez-vous aux liens suivants pour la sécuriser :

- https://dev.mysql.com/doc/refman/5.0/fr/security-against-attack.html
- http://www.mag-securs.com/News/tabid/62/id/17917/La-Securisation-des-bases-de-donnees-pour-eviter-de-divulguer-les-informations-privees-sur-Internet.aspx
- http://www.tux-planet.fr/securisation-d-un-serveur-mysql/

[fail2ban]: http://www.fail2ban.org/wiki/index.php/Main_Page "fail2ban - Site officiel"
[Ubuntu-fr]: http://doc.ubuntu-fr.org/fail2ban "Ubuntu-fr : fail2ban"
[Rootkit Hunter]: http://rootkit.nl/projects/rootkit_hunter.html "Rootkit Hunter - Site officiel"
[chkrootkit]: http://www.chkrootkit.org/ "chkrootkit - Site officiel"
