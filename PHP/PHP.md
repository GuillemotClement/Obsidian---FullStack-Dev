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

On viens ensuite itérer sur le tableau retourné par la fonction pour afficher uniquement les autheur souhaité sur la page :

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
