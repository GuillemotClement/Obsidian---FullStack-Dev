

---

# Seed de données

On commence par créer une fonction qui viens configurer le call HTTP. Cette fonction ne sera appelé qu'une seule fois lors du lancement de l'application.

On viendras utiliser cette fonction pour ajouter les première données dans l'application.

### Fonction seedRecipes()

On viens créer une nouvelle fonction asynchrone. Cette fonction effectuant une requêtes HTTP.

````javascript
import { data } from "./recipes";

export async function seedRecipes() {
  await fetch("https://restapi.fr/api/recipess", {
    //on indique la méthode de la requête
    method: "POST",
    //on indique le contenu de la requêtes
    headers: {
      // ici on envoie du JSON
      "Content-Type": "application/json",
    },
    // on passe dans le body un tableau json
    //on vient lui passer la tableau créer dans un autre fichier
    body: JSON.stringify(data),
  });
}
`````

On viens ensuite l'utiliser dans le composant `App`afin d'appeler la fonction au lancement de l'application.

````javascript
//App.jsx
import Header from "./components/Header/Header";
import Homepage from "./pages/Homepage/Homepage";
import Footer from "./components/Footer/Footer";
import styles from "./App.module.scss";

//importation de la fonction seed
import { seedRecipes } from "./data/seed";

//invocation de la fonction
//on viens la commenter une fois le seed réalisé
seedRecipes();

function App() {
  return (
    <div className={`d-flex flex-column ${styles.appContainer}`}>
      <Header />
      <Homepage />
      <Footer />
    </div>
  );
}
export default App;
`````

### Gestion du chargement d'articles

Dans cet exemple, on utilise le service Web API de Dyma. Etant donné que les données ne sont pas gardées pour une durée infinis, il est nécessaire de renvoyer les données de base de l'application.

Il sera nécessaire de gérer le temps que l'on récupères les données. Pour cela, on viens afficher un Gif de chargement le temps que la requêtes de récupération d'articles soit terminé.

On commence par créer une nouvelle variable d'état. On l'initialise à `true`car on viendras directement effectuer la requête pour récupérer les données du serveur.
````javascript
const [isLoading, setIsLoading] = useState(true);
`````

Pour la gestion de l'affichage, on viens utiliser un ternaire. 
On viens regarder la valeur de `isLoading`. Si elle est évalué à `true` alors on affiche le Git de chargement, sinon on affiche la liste de recette.

Dans le composant, on viens effectuer l'opération ternaire : 

````javascript 
return (
    <div className="flex-fill container d-flex flex-column p-20">
      <h1 className="my-30">Découvrez nos nouvelles recettes</h1>
      <div className={`card flex-fill p-20 d-flex flex-column mb-20 ${styles.contentCard}`}>
        <div
          className={`d-flex flex-row justify-content-center align-item-center my-30 ${styles.searchBar}`}
        >
          <i className="fa-solid fa-magnifying-glass mr-15"></i>
          <input
            type="text"
            placeholder="search ..."
            value={filter}
            className="flex-fill"
            onInput={handleInput}
          />
        </div>
        {isLoading ? (
          <div className="">
            <p>Recettes en cours de chargement</p>
            <i className="fa-solid fa-spinner fa-spin"></i>
          </div>
        ) : (
          <div className={styles.grid}>
            {recipes
              .filter((recipe) => recipe.title.toLowerCase().startsWith(filter))
              .map((recipe) => (
                <Recipe
                  key={recipe._id}
                  title={recipe.title}
                  picture={recipe.picture}
                />
              ))}
          </div>
        )}
      </div>
    </div>
  );
  `````
  
Pour plus de simpliciter, on vient créer un nouveau composant de chargement. On viens le placer dans le dossier `components` étant donné qu'il peut être placer sur toutes les pages de l'application.

```javascript
//Loading.jsx
import style from "./Loading.module.scss";

export default function Loading() {
  return (
    <div className="d-flex flex-row align-items-center justify-content-center flex-fill">
      <i className={`fa-solid fa-spinner fa-spin ${style.spinner}`}></i>
    </div>
  );
}
```

On viens ensuite utiliser ce composant dans la condition ternaire :

```javascript
{isLoading ? (
  <Loading />
) : (
  <div className={styles.grid}>
	{recipes
	  .filter((recipe) => recipe.title.toLowerCase().startsWith(filter))
	  .map((recipe) => (
		<Recipe
		  key={recipe._id}
		  title={recipe.title}
		  picture={recipe.picture}
		/>
	  ))}
  </div>
)}
```

