Avec React, on vient créer des application SPA, c'est à dire des applications que l'on ne vient charger qu'une seule fois. On ne viendras jamais recharger la page.

Pour récupérer des données, on viendras utiliser des requêtes HTTP de type AJAX qui sont des requêtes réalisé depuis JavaScript et qui ne nécessite pas de recharger la page.

Pour réaliser ses requêtes on viendras utiliser [[fetch()]] qui permet d'effectuer n'importe quel type de requête HTTP.
Cet API retourne ensuite une promesse qu'on viendras exploiter.

On retrouve cette syntaxe :
````javascript
const promesse = fetch(url, [options]);
````

`url` : c'est la cible de la requête. C'est le point que l'on souhaite atteindre
`options` : objet qui représente les options que l'on vient passer

La méthode `fetch()` retourne une promesse qui sera tenu si le serveur répond. Cette promesse est résolue avec un objet `Response`

[[POST]]
[[GET]]
[[PATCH]]
