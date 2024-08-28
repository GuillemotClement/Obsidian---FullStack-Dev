Dans ce chapitre, on vient mettre la place la persistance des likes des recettes de l'application.

Tout d'abord, on vient modifier l'objet contenant la recette en ajoutant une nouvelle propriété `like` qui contient une valeur boolena. Si `true` alors on affiche le coeur en orange, sinon le coeur reste en noir.

On viens depuis le composant `Recipe.jsx` faire différentes modification.

On retire l'utilisation du useState car on viendras récupérer les données depuis le serveur. On viens également faire passer la prorpiété dans le composant en tant que props.

Depuis le composant `Homepage.jsx`, on viendras transmettre directement l'ensemble de la recipe issus de la méthode `map()`.

````javascript
{recipes
.filter((recipe) => recipe.title.toLowerCase().startsWith(filter))
.map((recipe) => (
<Recipe
	  key={recipe._id}
	  recipe={recipe}
	/>
))}
````

Dans le composant `Recipe.jsx` on viendras de nouveau déconstruire pour récupérer les différentes propriétés souhaitées.

Pour effectuer une double déconstruction, on indique la clé, puis on déconstruit :

````javaScript
export default function Recipe({ recipe: { _id, liked, title, image } }) {
	...
}
````

De cette manière, on peut venir utiliser les différentes propriétés que l'on souhaite dans le composant

### Mise en place de la fonctionnalité

On viendras maintenant faire une requête pour indiquer la mise à jour de la valeur de la propriété `liked`.

La requête sera effectués dans la fonction `handleClick`. On viendras également faire une modification du composant `Homepage` pour indiquer une modification d'une valeur de Recipe.

On viens ajouter une nouvelle fonction permettant de mettre à jour la recette :

```javascript
function updateRecipe(updatedRecipe) {
		setRecipes(
		recipes.map((recipe) => (recipe._id === updatedRecipe._id ? updatedRecipe : recipe))
	);
}
```

On viens ensuite passer cette fonction dans le composant `Recipe` :

````javascript
{recipes
  .filter((recipe) => recipe.title.toLowerCase().startsWith(filter))
  .map((recipe) => (
	<Recipe
	  key={recipe._id}
	  recipe={recipe}
	  toggleLikedRecipe={updateRecipe}
	/>
  ))}
````

On vient maintenant réaliser le call depuis le composant `Recipe`

```javascript
  //on vient récupérer l'url de base via le context
  const BASE_URL_API = useContext(ApiContext);
  
  //on vient réaliser la requête pour la mise à jour de la propriété
  async function handleClick() {
    // configuration de la requete
    try {
      //on vient sélectionner un article avec son id pour modifier la valeur
      const response = await fetch(`${BASE_URL_API}/${_id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          liked: !liked,
        }),
      });
      if (response.ok) {
        const updateRecipe = await response.json();
        toggleLikedRecipe(updateRecipe);
      }
    } catch (e) {
      console.log("Erreur :", e);
    }
  }
```
