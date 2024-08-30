Un système de pagination permet de limiter le nombre d'éléments affiché sur une page par exemple. De cette manière, on réduit le nombre d'élément à télécharger lors des requetes pour récupérer des données.

Pour mettre en place ce système dans notre application, on viendras modifier le fonctionnement du fetch pour récupérer les différentes recettes.

On viens mettre en place un nouveau bouton qui permet de venir charger plus de contenu. Dans le composant `Homepage`, on ajoute ce bouton :

```javascript
<div className="d-flex flex-row justify-content-center align-items-center p-20">
  <button className="btn btn-primary">Charger plus de recettes</button>
</div>
```

On viens ensuite complexifier la requête en ajoutant des paramètres 

````javascript
const response = await fetch(`${BASE_URL_API}?limit=18`);
````

