
# Gestion des paquets

Pour les distributions GNU/Linux basées sur Debian, il existe principalement deux commandes pour gérer les paquets de votre système : `apt-get` et `aptitude`. Les commandes des autres distributions ne seront pas traitées ici mais leurs fonctionnements restent très similaires.

## apt-get

### Mise à jour

Avant toute manipulation de recherche ou d'installation, il faut mettre à jour les dépôts pour vous assurer de récupérer les dernières versions :

``` bash
sudo apt-get update
```

### Recherche de paquets

Pour vérifier qu'un paquet est disponible pour votre distribution GNU/Linux ou tout simplement pour rechercher un paquet spécifique, utilisez la commande suivante :

``` bash
sudo apt-cache search "nom-du-paquet"
```

### Installation de nouveaux paquets

Pour installer un paquet ainsi que ses dépendances de façon « automatique », tapez la ligne suivante :

``` bash
sudo apt-get install "nom-du-paquet"
```

### Suppression de paquets

Pour supprimer un paquet :

``` bash
sudo apt-get remove "nom-du-paquet"
```

Utilisez l'option *autoremove* qui supprime le paquet et ses dépendances devenues inutiles. Pour supprimer un paquet et ses fichiers de configuration :

``` bash
sudo apt-get purge "nom-du-paquet"
```

Pour supprimer un paquet, ses dépendances et ses fichiers de configuration :

``` bash
sudo apt-get autoremove --purge "nom-du-paquet"
```

### Mise à jour

Si vous souhaitez mettre à jour un ou des paquets spécifiques, vous pouvez utiliser la commande suivante :

``` bash
sudo apt-get install "nom-du-paquet"
```

La commande suivante permet d'installer les versions les plus récentes de tous les paquets présents sur le système. Les paquets installés pour lesquels il existe de nouvelles versions sont récupérés et mis à niveau. En aucun cas des paquets déjà installés ne sont supprimés. De même, des paquets qui ne sont pas déjà installés ne sont ni récupérés, ni installés. Les paquets dont de nouvelles versions ne peuvent pas être installées sans changer le statut d'installation d'un autre paquet sont laissés dans leur version actuelle.

``` bash
sudo apt-get upgrade
```

L'option *dist-upgrade* effectue la fonction *upgrade* en y ajoutant une gestion intelligente des changements de dépendances dans les nouvelles versions des paquets. Autrement dit, à l'inverse de la commande précédente, *dist-upgrade* peut installer de nouveaux paquets si cela est nécessaire pour la mise à jour des paquets existants.

``` bash
sudo apt-get dist-upgrade
```

### Nettoyage

Pour supprimer le cache des paquets installés qui n'est plus nécessaire :

``` bash
sudo apt-get autoclean
```

Afin de nettoyer entièrement le cache :

``` bash
sudo apt-get clean
```

### Sources

Le fichier de configuration indiquant à la commande où se trouvent les sources des paquets se situe à l'emplacement suivant :

``` bash
sudo nano /etc/apt/sources.list
```

### Les options

Reportez-vous au manuel de la commande `apt-get` pour plus d'informations car les options sont trop nombreuses pour en faire une liste exhaustive ici. Voici les plus utiles :

| Option        | Signification     | Détail                                                                                            |
| :------------ | :---------------- | :------------------------------------------------------------------------------------------------ |
| *-d*          | *download-only*   | Télécharge les paquets mais ils ne sont ni dépaquetés, ni installés.                              |
| *-s*          | *simulate*        | Pas d'action, simule les évènements qui devraient se produire mais sans effectuer de changement.  |
| *-y*          | *yes*             | Répond automatiquement par oui aux questions posées pendant le processus.                         |
| *-b*          | *build*           | Cette commande compile un paquet source après l'avoir récupéré.                                   |
| *-v*          | *version*         | Affiche la version du programme.                                                                  |

## Aptitude

Cette commande est un gestionnaire de paquets basé sur l'infrastructure APT, c'est-à-dire que vous pouvez installer, supprimer et mettre à jour des commandes (paquets). Elle présente des fonctionnalités équivalentes à `dselect` ou `apt-get`. Il y a deux façons d'utiliser `aptitude` : la première, en ligne de commande, est semblable à `apt-get` où l'on retrouve les mêmes options ; l'autre passe par l'interface interactive. La commande `aptitude` est plus récente que `apt-get` mais cette dernière est encore largement utilisée. Il est préférable de faire un choix entre ces deux gestionnaires et de n'utiliser que celui qui est retenu. Ceci évitera, par exemple, de mélanger les configurations de chacune de ces commandes.

Attention, sur certaines distributions, `aptitude` n'est pas installé. Il faut donc passer par la commande :

``` bash
sudo apt-get install aptitude
```

### Ligne de commande

#### Mise à jour des dépôts

Quand vous souhaitez rechercher ou installer un paquet, il faut mettre à jour les dépôts afin d'avoir accès aux dernières versions des paquets. Utilisez la commande suivante : 

``` bash
sudo aptitude update
```

#### Recherche de paquets

Pour vérifier qu'un paquet est disponible sur votre distribution GNU/Linux ou tout simplement pour rechercher un paquet spécifique, utilisez la commande suivante :

``` bash
sudo aptitude search <Expression rationnelle>
```

Il est possible de rechercher une version en particulier d'une commande demandée :

``` bash
sudo aptitude versions "nom-du-paquet"
```

#### Informations de paquets

Il est possible de vérifier si une commande est installée et d'obtenir des informations sur celle-ci :

``` bash
sudo aptitude show -v "nom-du-paquet"
```

L'option *v* (pour *verbose*) donnera plus de détails.

Il est également possible d'afficher les versions disponibles d'un paquet :

``` bash
aptitude versions "nom-du-paquet"
```

#### Installation de paquets

Pour installer un paquet ainsi que ses dépendances « automatiques », tapez la ligne suivante :

``` bash
sudo aptitude install "nom-du-paquet"
```

#### Suppression de paquets

Il est possible de marquer des paquets qui seront alors identifiés par la commande `aptitude`. De ce fait, quand vous désinstallerez des commandes, les paquets ainsi marqués seront supprimés dès lors‏ qu'aucun autre paquet installé sur votre système ne fera plus référence à ces derniers :

``` bash
sudo aptitude markauto "nom-du-paquet"
```

Pour supprimer un paquet, ainsi que ses dépendances « automatiques » devenues inutiles :

``` bash
sudo aptitude remove "nom-du-paquet"
```

Pour supprimer un paquet et ses fichiers de configuration :

``` bash
sudo aptitude purge "nom-du-paquet"
```

#### Mise à jour de paquets

Pour télécharger les mises à jour des paquets installés sur votre système :

``` bash
sudo aptitude safe-upgrade
```

Mettre à jour les paquets :

``` bash
sudo aptitude update
```

#### Mise à jour du système

Pour réaliser une mise à jour complète de votre système ainsi que de tous les paquets installés : 

``` bash
sudo aptitude full-upgrade
```

Attention, l’option *full-upgrade* peut supprimer des paquets pour en installer de nouveaux et est donc moins conservatrice que *safe-upgrade*.

#### Nettoyage

Pour supprimer tous les paquets *.deb* téléchargés et enregistrés dans le répertoire cache (normalement `/var/cache/apt/archives`), utilisez la commande suivante :

``` bash
sudo aptitude clean
```

Pour éviter que le cache ne grossisse démesurément avec le temps mais en évitant tout de même d'avoir à le vider complètement, vous pouvez supprimer tout paquet enregistré dans le cache et qui n'est plus proposé au téléchargement avec la commande :

``` bash
sudo aptitude autoclean
```

#### Verrouiller un paquet

Pour annuler toute action de *self-upgrade* ou *full-upgrade* d'un paquet, utilisez la commande :

``` bash
sudo aptitude hold "nom-du-paquet"
```

Pour revenir en arrière :

``` bash
sudo aptitude unhold "nom-du-paquet"
```

### Interface interactive

Pour accéder à l'interface interactive de `aptitude` :

``` bash
sudo aptitude
```

Vous serez alors face à une liste de paquets, classés par état. Une fois dans l'interface interactive, vous pourrez installer des paquets, en supprimer, faire des mises à jour, etc. à l'aide des touches du clavier. Pour quitter, appuyez sur <kbd>q</kbd> et confirmez en appuyant sur <kbd>o</kbd>.

#### Installation de paquets

Pour installer un paquet, vous devez faire comme avec Synaptic : le rechercher, le sélectionner pour l'installation puis appliquer les changements. Pour rechercher un paquet, appuyez sur <kbd>/</kbd>. Vous serez alors face à une boite de recherche : entrez le nom du paquet, la recherche se lance automatiquement. Une fois que le nom est écrit au complet, appuyez sur <kbd>ENTRÉE</kbd>. Si ce n'est pas le paquet correspondant, appuyer sur <kbd>n</kbd> pour rechercher le paquet suivant qui contient les termes recherchés, jusqu'à ce que vous trouviez le paquet à installer. Lorsque le paquet est trouvé, appuyez sur la touche <kbd>+</kbd> pour le sélectionner et l'ajouter à l'installation. Les dépendances seront automatiquement sélectionnées. Pour confirmer les changements, appuyez sur <kbd>g</kbd> et appuyez de nouveau sur <kbd>g</kbd> pour confirmer ou sur <kbd>q</kbd> pour revenir à l'écran précédent.

En résumé :

- « / » lancer une recherche
- « n » poursuivre la recherche (*next*)
- « + » sélectionner pour installation
- « = » maintenir le paquet dans sa version actuelle
- « g » (première fois) confirmer les changements (*go*)
- « g » (deuxième fois) appliquer les changements (*go*)

#### Suppression de paquets

On cherche le paquet avec <kbd>/</kbd>, puis on le sélectionne pour le supprimer avec <kbd>–</kbd> (suppression simple) ou alors avec <kbd>_</kbd> pour supprimer les fichiers de configuration en même temps. Enfin confirmer avec <kbd>g</kbd> et confirmer l'action de nouveau avec <kbd>g</kbd>. Vous remarquerez que les paquets qui avaient été installés automatiquement par `aptitude` pour satisfaire les dépendances sont automatiquement supprimés s'ils ne sont plus utilisés.

En résumé :

- « – » supprimer simplement (`apt-get remove`)
- « _ » supprimer le paquet et ses fichiers de configuration (`apt-get remove –purge`)
- « = » maintenir le paquet dans sa version actuelle
- « g » (première fois) confirmer les changements (*go*)
- « g » (deuxième fois) appliquer les changements (*go*)

#### Mise à jour

Pour une mise à jour de la liste des paquets disponibles, il suffit d'appuyer sur <kbd>u</kbd>. Pour mettre à jour les paquets qui peuvent l'être, appuyez sur <kbd>U</kbd>, puis sur <kbd>g</kbd> pour confirmer et une autre fois pour appliquer. Pour mettre à jour seulement un paquet dans tous ceux qui peuvent être mis à jour, faites comme si vous vouliez l'installer : lancez une recherche puis appuyez sur <kbd>+</kbd>, <kbd>g</kbd> et encore <kbd>g</kbd>.

En résumé :

- « u » mettre à jour la liste des paquets (`apt-get update`)
- « g » (première fois) confirmer les changements (*go*)
- « g » (deuxième fois) appliquer les changements (*go*)

##### Sources

- [Ubuntu-fr : Les dépôts APT](http://doc.ubuntu-fr.org/depots "Ubuntu-fr : Les dépôts")
- [Ubuntu-fr : aptitude](http://doc.ubuntu-fr.org/aptitude "Ubuntu-fr : aptitude")
- [Ubuntu-fr : apt-get](http://doc.ubuntu-fr.org/apt-get "Ubuntu-fr : apt-get")
- [Manuel de aptitude en ligne](http://algebraicthunk.net/~dburrows/projects/aptitude/doc/fr/index.html "Manuel de aptitude en ligne")
