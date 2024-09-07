---
created: 
tags: []
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

## Premier fichier PHP

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

## Types de données

[[Type de données PHP]]

### Chaîne de caractère

#### Déclaration d'une chaîne de caractère

Pour déclarer une chaîne de caractère on pourras utiliser `'` ou bien `"`.

```php
<?php
	echo "Hello World";
?>
```

En utilisant `"` pour une chaîne de caractère, une variable sera pris en compte, et c'est la valeur stockée dans la variable qui sera affiché.

#### Concaténation 

En PHP, pour concaténer, on utilise l'opérateur `.`

```php
<?php
	echo "Hello, " . "World";
?>
```

Ici, on viens fusionner les deux chaînes pour en former qu'une seule.

On peut très bien venir fusionner deux chaînes de caractères, mais également une chaîne avec une variable pour rendre cela dynamique.

```php
<?php 
	$name = "Clément";

	echo "Hello " . $name; //Hello Clément
?>
```

#### Syntaxe alternative

On pourras utiliser une syntaxe alternative en utilisant les `"` pour déclarer une chaîne. Dans ce cas, la variable sera directement pris en compte, et c'est la valeur qui sera affiché dans le navigateur.

Dans le cas ou l'on utilise `'`, la variable sera affiché comme tel, sans être pris en compte
```php
<?php 
	$name = "Clément";
	echo "Hello, $name";
?>
```

On obtient le même affichage dans le navigateur.
Cette syntaxe simplifie le code. 

On viens utiliser `"` dans le cas ou l'on souhaite insérer des variable dans une chaîne.

#### Insérer du PHP dans une balise HTML

On pourras venir afficher la valeur d'une variable dans une balise HTML.

```php
<?php 
	$name = "Jean";
?>

<h1>
	Ton nom est "<?php echo $name; ?>"
</h1>


```

#### Syntaxe simplifié

On pourras également utiliser une syntaxe simplifié. 

```php 
<h1>
	<?= $message; ?>
</h1>
```

Dans cette syntaxe, on supprime `php echo`. On utilise un `=` à la place.

#### Silo de variable

Dans le cas ou l'on souhaite mettre en 'silo' une variable, on pourras la placer entre `{}`. 

```php
echo "<li>{$book}TM</li>";
```

## Variable PHP

Tout ce qui se trouve entre les balises ouvrante et fermantes PHP sont considérer comme du PHP.
Les variables devront donc être utilisé au sein des balises PHP.

### Déclarer des variables en PHP

Pour déclarer une variable, on utilise `$`puis le nom de la variable.

On pourras ensuite affecter une valeur à la variable.

```php
<?php 
	$name = "Clément";
?>
```


# Condition & Boolean

## Boolean

Les boolean sont un type de données qui prends en valeur `true` ou `false`.

```php
<?php 
	$isRed = true;
?>
```

## Condition

Les conditions permettent d'effectuer dans actions selon la valeur boolean d'une variable.

### Déclarer une condition

#### if

On utilise le mot clé `if` puis des parenthèses. Ce qui est placé entre les parenthèse est la valeur que l'on vient checker.

Si la valeur est évalué à `true`, alors le code placé dans le bloc (entre les crochets) est exécuté.

```php
if(condition){
	echo "La valeur est true";
}
```

#### else

On pourras exécuter le mot clé `else` pour exécuter du code dans le cas ou la condition est évalué à `false`

```php
if(condition){
	echo "La valeur est true";
}else{
	echo "La valeur est false";
}
```

#### else if

On pourras venir évaluer plusieurs condition avec le mot clé. Dans le cas ou la première évaluation est évalué à `false`, alors on vient tester la `else if`suivant et ainsi de suite.

```php
if(condition){
	echo "La valeur est true";
}else if(condition2){
	echo "La valeur de condition2 est true";
}else{
	echo "La valeur est false";
}
```

#### Exemple d'utilisation 

Dans l'exemple, on déclare trois variables.
- `$name`: contient le nom du livre 
- `$isRead`: contient un boolean. 
- `$message`: contient un message indiquant si le livre est lu ou non

On vient faire une condition. Celle ci modifie la valeur de `$message`selon si le livre à été lu par un utilisateur.

On vient ensuite afficher la valeur de `$message` sur la page.

```php
<body>
	<?php
		$name = "The Bible";
		$isRead = false;
		//pour eviter des bug, on initialise la variable avec une chaîne vide
		$message = "";
	
		if($isRead) {
			$message = "Vous avez lu $name";
		} else {
			$message = "Vous n'avez pas lu $name";
		}
	?>
	
	<h1>
		<?= $message; ?>
	</h1>
</body>
```

### Opérateur de comparaison 

#### Egalité 

Pour vérifier si une valeur est égale à une autre, on utiliseras l'opérateur `==` ou bien `===`.
Dans le cas où l'on utilise trois `=`, on effectue une comparaison strict.
C'est à dire que la valeur et le type de la donnée est pris en compte
## Array 

Les tableaux permettent de stocker une collection de données. Par exemple, une liste des livres préférés d'un utilisateur.

On pourras venir stocker n'importe quel type de données dans un tableau (string, number, boolean, array).
### Déclarer un array 

Pour déclarer une nouveau tableau, on viens utiliser les crochets :

```php
$books = [];
```

On pourras déclarer des valeurs directement dans ce tableau :

```php 
$books = [
	"1984 (1949)",
	"Dune (1965)",
	"Fondation - Le Cycle de Fondation, tome 1 (1951)"
];
```

Entre chaque valeurs, on viens ajouter une virgule pour séparer chacune d'elle.

### Afficher le contenu d'un tableau 

Une fois le tableau déclaré, on pourras venir le parcourir pour afficher son contenu sur la page.

#### foreach

Pour itérer et afficher chaque élément du tableau, on vient utiliser `foreach`. Cette boucle vient itérer sur chaque élément du tableau.

```php
<ul>
	<?php foreach($books as $book): ?>
		<li><?= $book ?></li>
	<?php endforeach ?>
</ul>
```
- `$books` : est le nom du tableau sur lequel on souhaite itérer
- `$book`: contient la valeur de l'élément en cours d'itération

On viens ensuite afficher un élément `<li>` avec la valeur contenu dans le tableau.

![[Pasted image 20240906160829.png]]

### Afficher un élément du tableau 

On pourras venir afficher un élément précis du tableau en utilisant l'index de cet élément.

L'index représente l'emplacement de la valeur que l'on souhaite. Un tableau commence toujours avec un index à 0.

On viens indiquer l'index entre crochet. 

```php
<body>
	<h1>Recommanded Books</h1>
	<?php
		$books = [
			"1984 (1949)",
			"Dune (1965)",
			"Fondation - Le Cycle de Fondation, tome 1 (1951)",
			"Le Meilleur des mondes (1931)"
		];
	?>
	
	<p>
		<?= $books[1] ?>
	</p>
</body>
```

Dans l'exemple, on vient afficher sur la page uniquement le second élément du tableau.

## Tableau associatif

Les tableaux associatif sont l'équivalent des objets en JS. Il permet d'ajouter des clé à des valeurs.
Chaque clé étant associé à une valeur. 

On vient utiliser la `camelCase`pour les clé.

### Déclarer un tableau associatif

De la même façon que pour un tableau basique, on utilise les crochets :

```php 
<?php
	$books = [
		[
			"name" => "1984",
			"author" => "George Orwell",
			"year" => 1949,
			"purchaseUrl" => "https://www.amazon.fr/1984-George-Orwell"
		],
		[
			"name" => "Dune",
			"author" => "Frank Herbert",
			"year" => 1965,
			"purchaseUrl" => "https://www.amazon.fr/Dune-1-Frank-HERBERT"
		]
	];
?>
```

### Affecter une nouvelle valeur 

On pourras affecter une nouvelle valeur en désignant le tableau, avec sa clé dans les crocnet, et en lui affectant une nouvelle valeur 

```php 
$book['name'] = "Mon nouveau titre de livre";
```


### Afficher les éléments du tableau 

On ne pourras pas directement utiliser le `foreach`sur un tableau associatif.

On pourras venir utiliser la clé de l'élément que l'on souhaite utiliser :

```php
<ul>
	<?php foreach($books as $book): ?>
		<li><?= $book['name'] ?></li>
	<?php endforeach ?>
</ul>
```

Dans ce code, on vient afficher uniquement le nom des éléments dans le tableau associatif.

On pourras venir afficher plusieurs élément du tableau :

```php 
<ul>
	<?php foreach($books as $book): ?>
		<li>
			<a href="<?= $book['purchaseUrl'] ?>" target="_blanck">Link to buy</a>
			<span><?= $book['name'] ?></span>
		</li>
	<?php endforeach ?>
</ul>
```

### Parcourir un tableau dans un tableau 

Dans le cas ou une clé contient un tableau, il sera très simple de parcourir chaque élément du tableau interne.

```php
$business = [
	'name' => "Laracast",
	'price' => 15,
	'categories' => ['Testing', 'Javascript', 'PHP']
];

foreach($business['categories'] as $category){
	echo $category . '<br/>';
}
```


## Fonction 

### Déclaration d'une fonction 

Pour déclarer une fonction, on vient utiliser le mot clé `function`. Dans les parenthèse on vient indiquer les paramètres que l'on souhaite utiliser.

On utilise le mot clé `return`dans la fonction pour récupérer une valeur.

```php
function filterByAuthor(parameter){
	//code execute when funcion is call
}
```

Une fois la fonction déclaré, il faut venir l'appeler pour exécuter le code dans le bloc de fonction

### Appeler une fonction

Pour utiliser une fonction, on utilse son nom, et on lui passe des valeurs dans l'ordre des paramètres.

```php
filterBuAuthor();
```

#### Mise en pratique

On viens créer une fonction qui filtre les auteurs. 

La fonction prend deux paramètre : un tableau de livre et un nom d'auteur

```php 
function filterByAuthor($books, $author){
	//on créer un tableau vide qui contiendras les éléments filtrés
	$filterBooks = [];
	//on parcourt le tableau de livres
	foreach($books as $book){
		//on vient faire la condition selon l'auteur passé en argument
		if($book['author'] === $author){
		//si la condition est true, alors on ajoute l'élément dans le tableau
		$filterBooks[] = $book;
		}
	}
	//une fois le tableau de livre itérer, on retourne le nouveau tableau
	return $filterBooks;
}
  
//on créer une variable contenant le nom de l'auteur que l'on souhaite
$author = "Frank Herbert";

//on créer une variable contenant le tableau filtré retourné par la fonction
$filterBooksByAuthor = filterByAuthor($books, $author);
```

On viens ensuite itérer sur le tableau retourné par la fonction pour afficher uniquement les auteur souhaité sur la page :

```php 
<ul>
	<?php foreach($filterBooksByAuthor as $book): ?>
		<li>
			<a href="<?= $book['purchaseUrl'] ?>" target="_blanck">
				<?= $book['name'] ?> - <?= $book['releaseYear'] ?>
			</a>
		</li>
	<?php endforeach ?>
</ul>
```

#### Refacto 

On pourras refactoriser la fonction de filtre pour la rendre plus générique :

```php
//$data étant le tableau de données
//$key étant ce que l'on souhaite filtré
//$value étant la valeur que l'on veut récupérer
function filter($data, $key, $value){
	$filterData = [];
	
	foreach($data as $item){
		if($item[$key] === $value){
			$filterData[] = $item;
		}
	}
	
	return $filterData;
}

$filteredBooks = filter($books, 'author', 'Asimov Isaac');
```

On peut ensuite venir traiter la données retourner dans un tableau par la fonction `filter()`


### Fonction anonyme 

On pourras utiliser des fonctions anonymes. On stocke la fonction dans une variable.

On pourras venir appeler une fonctio anonyme en la passant dans ces paramètres.

Avec cette fonctionnalité, on pourras rendre la fonction `filter()`encore plus générique.

-> wtf faut revenir la dessus https://laracasts.com/series/php-for-beginners-2023-edition/episodes/9


## Séparer le logique du template

Pour garder une bonne organisation dans le code, on viens séparer le PHP du HTML.

Dans l'exemple, on retrouve du code PHP au milieu du fichier HTML. Ceci n'est pas une bonne pratique.

Pour avoir une bonne base de code qui reste maintenanble, on viendras séparer le code PHP du code HTML.

### PHP et HTML

La base d'une bonne séparation est de placer le code PHP (fonction, data) tout en haut du document.
On viendras ajouter le HTML à la suite du code PHP.

On conserve uniquement la partie responsable de l'affichage dans le code HTML (foreach par exemple). Ce code devra rester le plus simple possible. Toute la partie logique sera exécuté dans la partie placer en haut du document.

### Fichier séparé

Avec le temps, l'application viens grossir de plus en plus. Pour garder une base de code propre, on viens alors séparer le code PHP en plusieurs fichier. 
On viens ensuite importer les fichiers au endroit ou il seront utilisé.

Par exemple, pour notre exemple, on aurai un fichier contenant la logique PHP, et un fichier contenant le code HTML.
La partie HTML est appelé `view` ou `template` généralement.

Dans le cas ou le fichier ne contient que du code PHP, il n'est pas nécessaire d'ajouter la balise PHP fermante.

#### Convention de nommage

Pour les fichier contenant le HTML, on viens généralement appeler celui ci `name.view.php`, le `name`étant remplacé par le nom de la page correspondant.

#### Importer un fichier

Pour importer un fichier dans un autre fichier, on utilise le mot clé `require` ou `include`. 

Si on utilise `require`, alors il est obligatoire d'avoir le fichier sinon cela provoque une erreur.

Dans l'exemple, on as le fichier `index.php`qui contient toute la logique de l'application. Ici uniquement la tableau de livre, et la fonction de filtre.
On viens ajouter sur la dernière ligne du fichier :
```php
require "index.view.php";
```

Cette ligne permet d'importer le fichier HTML, et ainsi d'afficher la page avec les éléments souhaité.

# Dynamic Web Application

## II - Page Links

On pourras venir utiliser un skeleton de Tailwind UI pour aller plus vite.

### Créer plusieurs pages

On viens créer pour chaque nouvelle page que l'on souhaite, un nouveau fichier PHP. 

Par exemple, un fichier `contact.php` et un fichier `about.php`. On viens ensuite pour ces deux pages, créer un fichier view : `contact.view.php` et `about.view.php`.

Dans chacun des deux fichiers, on viens `require` le template correspondant.

### Créer des liens pour naviguer

Dans chaque fichier `view`, on viens coller le skeleton de tailwind pour obtenir une page correct. Dans la partie `nav`, on viens créer un lien qui pointe sur le fichier php qui correspond à la page que l'on souhaite afficher :

```php 
<div class="ml-10 flex items-baseline space-x-4">
	<a href="/" class="rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white" aria-current="page">Home</a>
	<a href="./about.php" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">About us</a>
	<a href="./contact.php" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">Contact</a>
</div>
```
On viens copier ce code dans chaque page de notre application.

## Partials 

Les partials permettent de simplifier l'écriture d'une page web. 

On viens écrire le code une fois, et on viens ensuite importer le morceau de code correspondant. De cette manière, il n'y a plus besoin de dupliquer le code.

### Organisation du dossier

Pour garder une base de code propre, on vient réorganiser la structure du dossier.

On viens créer un nouveau folder `views`qui contient les différents templates de notre application.

Dans ce folder, on viens créer un sous dossier `partials`qui sera utilisé pour stocker des partie spécifique d'une page.

Pour notre exemple, on viens récupérer la partie `<nav>`. On viens appeler ce fichier `nav.php`

### Importer un partial 

Pour importer le nouveau partial, on viens utiliser un `require`.

```php
<?php require ('partials/nav.php') ?>
```

De cette manière, on as qu'une seul fichier de code qui gère la navigation, et il n'y as pas besoin de dupliquer de code.

#### Navigation dynamique

Dans le cas de notre nav, on souhaite mettre en place un style dynamique selon la page sur lequel se trouve l'utilisateur.

Pour cela, on viens utiliser un contrôler. Son rôle est de définir quel données sont à affiché de manière dynamique.

## Superglobals & Current Page

### Modifier un style pour la navigation

On pourras utiliser les superglobal pour savoir si quel page on se trouve. On pourras ainsi ajouter un style particulier dans le cas ou l'on se situe sur une page.

#### Afficher le contenu d'un array

En PHP, on pourras venir afficher le contenu d'un tableau avec la fonction `print_r()`. 

Pour l'afficher correctement, ce tableau devras être placer encore les balise `<pre>`. De cette manière on conserve le formatage pour lire plus facilement le tableau.

```php 
echo "<pre>"
print_r($_SERVER);
echo "</pre>"
```

On pourras également utiliser `var_dump`

### Superglobal

Les surperglobals sont des variables accessible depuis n'importe quel endoit de notre application.

#### $_SERVER 

Cet superglobal permet de récupérer des informations sur la page actuel.


