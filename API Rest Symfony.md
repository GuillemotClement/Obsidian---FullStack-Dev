# Création du nouveau projet

On commence par créer un nouveau projet Symfony.

Etant donné que l'on souhaite créer une API Rest avec Symfony, il n'est pas nécessaire d'installer la version web complète. On utilise donc la version basique.

````bash 
symfony new nameProject 
````` 

Une fois le projet créer, on peut venir lancer le serveur avec la commande :

````bash 
symfony server:start
````` 

On peut maintenant se connecter sur le localhost de Symfony.

## Création première entité

On vient maintenant créer la première table de notre API.

### Installation maker-bundle

On viendras installer `maker-bundle` afin d'utiliser les script de Symfony et simplifier le travail.

````
composer require --dev symfony/maker-bundle
````

Installer ce bundle permet d'utiliser les différentes commande comme `make:controller`, `make:entity`, etc 

### Installation Doctrine

Pour venir installer Doctrine, on viens utiliser la commande :

````
composer require symfony/orm-pack
````

On viens ensuite configurer les informations pour se connecter à la base de données.

On vient ensuite créer la nouvelle DB :

`php bin/console doctrine:database:create`

### Création de la nouvelle table

Une fois la DB créer, on peut maintenant créer une nouvelle table :

`php bin/console make:entity`
