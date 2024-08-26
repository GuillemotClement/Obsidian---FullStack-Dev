

---

## Récupération des données

### Fetch initial

Pour le fetch initial, on viens utiliser un `effect`.

On commence par venir le déclarer :

```javascript
//on vient utiliser un useEffect qui viendras s'exécuter une seule fois. On viens la passer un tableau de dépendances vide.
useEffect(() => {}, []);
```

On viendras déclarer dans ce hook, une fonction asynchrone permettant de récupérer les données depuis le serveur

```javascript
//on vient utiliser un useEffect qui viendras s'exécuter une seule fois. On viens la passer un tableau de dépendances vide.
  useEffect(() => {
    //on viens verif si il faut faire un call
    let cancel = false;
    async function fetchRecipes() {
      try {
        setIsLoading(true);
        // on vient faire la requête pour récupérer les données
        const response = await fetch("https://restapi.fr/api/recipess");
        if (response.ok && !cancel) {
          //on vient récupèrer les recettes dans recipes
          const recipes = await response.json();
          //si la réponse est un tableau
		  //si true on retourne le recipes
          //sinon on ajoute dans un nouveau tableau
          setRecipes(Array.isArray(recipes) ? recipes : [recipes]);
        }
      } catch (e) {
        console.log("Erreur :", e);
      } finally {
        if (!cancel) {
          setIsLoading(false);
        }
      }
    }
    //on vient appeler la fonction d'appel
    fetchRecipes();
    //on viens utiliser une fonction de clean up
    return () => (cancel = true);
  }, []);
```

### Amélioration URL

On peut venir améliorer le processus en venant stocker le début de l'url que l'on souhaite atteindre. De cette façon, on réduit le nombre d'erreur potentiel.

Pour stocker l'url, on peut venir utiliser le `context` qui permet de récupérer de la données depuis n'importe où dans l'application.

Dans notre projet, on vient créer un nouveau dossier `context`. Ce folder permet de venir stocker tous les context utiliser dans l'application.

Ici, on viens l'appeler `ApiContext.js`. 

Dans ce fichier, on viendras créer le context

```javascript
import { createContext } from "react";

//on vient créer le context et on lui passe en valeur initial 'null'
export const ApiContext = createContext(null);
```

On viendras ensuite `provide` la nouvelle valeur de l'url depuis le composant `main.jsx` . Cela permet de rendre la valeur disponible dans toute l'application :

```Javascript
createRoot(document.getElementById("root")).render(
  <StrictMode>
    <ApiContext.Provider value="https://restapi.fr/api/recipess">
      <App />
    </ApiContext.Provider>
  </StrictMode>
);
```

On vient ensuite adapter la requête dans le composant `Homepage` pour l'utilisation du context. 
On viendras appeler la constante en majuscule pour indiquer que celle ci ne change pas dans le temps.

```JavaScript
const BASE_URL_API = useContext(ApiContext);
```

On pourras ensuite adapter la requête :

```` Javascript
useEffect(() => {
    //on viens verif si il faut faire un call
    let cancel = false;
    async function fetchRecipes() {
      try {
        setIsLoading(true);
        // on vient faire la requête pour récupérer les données
        const response = await fetch(BASE_URL_API);
        if (response.ok && !cancel) {
          //on vient récupèrer les recettes dans recipes
          const recipes = await response.json();
          //si la réponse est un tableau
          //si true on retourne le recipes
          //sinon on ajoute dans un nouveau tableau
          setRecipes(Array.isArray(recipes) ? recipes : [recipes]);
        }
      } catch (e) {
        console.log("Erreur :", e);
      } finally {
        if (!cancel) {
          setIsLoading(false);
        }
      }
    }
    //on vient appeler la fonction d'appel
    fetchRecipes();
    //on viens utiliser une fonction de clean up
    return () => (cancel = true);
  }, []);
````

