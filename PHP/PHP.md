---
created: 
tags:
  - PHP
---
---

```table-of-contents
```
# PHP

## Installation PHP

### Mac & Linux

https://brew.sh/

Pour installer PHP sur mac, on passeras par `Homebrew`qui est le gestionnaire de package sur Mac.

Ici, on utilise le terminal `Warp`. 
On commence par installer `Homebrew`qui permet d'installer les package nécessaire pour l'installation de PHP.

#### Chercher les paquet de PHP

On commence par lancer la commande : 

```shell
$ brew search php
```

Cette commande retourne tous les paquets que l'on peut venir installer. 

#### Lancer l'installation de PHP

Ici, on viens lancer la commande : 

```shell
$ brew install php
```

#### Vérifier si PHP est bien installer 

On viens lancer la commande :

```shell
$ php -v 
```

Cette commande retourne la version installé de PHP sur notre machine.

#### Installation MySQL

Ici, on viens ensuite installer MySQL en complément de PHP.

De la même manière, on viens utiliser `HomeBrew`pour l'installer :

```shell
$ brew install mysql
```

#### Lancer le service MySQL

Uen fois MySQL installé, il faudras venir le lancer. Dans le cas contraire, on obtient une erreur :

`ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)`

Pour lancer le service, on lance la commande :

```shell 
brew services start mysql
```

Une fois la commande lancé, le service MySQL sera lancer.

Pour vérifier que MySQL soit bien en service, on utilise la commande :

```shell
$ mysql
```

La commande permet de se connecter sur le serveur MySQL.

### Windows 

Pour Windows, on viendras utiliser `Laragon`pour gérer l'installation de PHP & MySQL.

https://laragon.org/download/

## MySQL

On viens ensuite choisir un logiciel pour avoir un UI potable pour l'utilisable de `MySQL`

Il existe deux options principales : 
- TablePlus : https://tableplus.com/
- PhpMyAdmin : https://www.phpmyadmin.net/

## First Tag

### Création d'un dossier pour le projet

On commence par créer un folder qui viens contenir les différents fichiers du projet. On viens créer un nouveau dossier dans `¬/` directement. Celui ci contiendras tous nos sites.

```shell
$ mkdir websites
```

On vient ensuite dans ce nouveau folder 

```shell
$ cd websites
```

On viens ensuite créer un nouveau folder qui contient notre nouveau projet.

```shell 
$ mkdir helloWorld
$cd helloWorld
```

On viens maintenant ouvrir ce folder directement dans VSCode.

#### Premier fichier

On viens créer un nouveau fichier `index.html` :

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta
		name="viewport"
		content="width=device-width, initial-scale=1.0"
		/>
		<title>Hello World</title>
	</head>
		<body>
			<h1>Hello World</h1>
		</body>
</html>
```

Il faudras toujours avoir un fichier `index`dans un repertoire car celui ci est le point d'entrée du site web

#### Afficher l'aide commande php

Pour afficher la manuel de la commande php, on viens lancer :

```shell
$ php -h
```

La commande retourne la liste des commandes disponible.

#### Lancer le serveur local PHP

Pour lancer le serveur local PHP, on viendras lancer la commande :

```shell 
$ php -S localhost:8000
```

Une fois la commande lancé, le serveur local PHP est lancé.

Il faudras lancer la commande depuis le répertoire du projet. 

#### Premier fichier PHP

Pour avoir un site dynamique, on viens renommer le fichier `index.html`en `index.php` .

On pourras venir utiliser du PHP dans ce fichier.

Pour écrire une instruction en PHP, on utilise les balises `<?php ?>`

#### Afficher un élément 

Dans les balise php, on viens utiliser l'instruction `echo`

Pour afficher quelque chose en PHP, on utilise l'instruction `echo` , puis entre `"` indiquer le texte que l'on souhaite afficher.

```php
//ouverture bloc code PHP
<?php
	//instruction PHP
	echo "Hello World";
//fermeture bloc PHP
?>
```

Une instruction PHP se termine toujours pas un `;`. 