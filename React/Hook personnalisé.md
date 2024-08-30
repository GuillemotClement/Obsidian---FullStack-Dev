
## I - Qu'est ce qu'un hook personnalisé

### Utilité 

Les hook personnalisés permettent d'extraire la logique d'un composant sous forme de fonctions réutilisable.

Il permettent la composition de `hooks`. On viendras utiliser des hooks au sein d'une fonction. Cette fonction sera ensuite utilisé au sein d'un composant React.

Cette fonctionnalité permet d'obtenir une meilleure lisibilité du composant, et permet une réutilisabilité de la logique.
### Composition

La composition de fonction est un paradigme de la programmation fonctionnelle qui permet de combiner des fonctions simples pour obtenir des comportements plus complexes.

### Caractéristiques


Une fonction est considérée comme un hook à partir du moment ou elle répond à ces critères : 
- le nom est préfixé par `use`
- la fonction doit utiliser les hooks au plus haut niveau de la fonction
- le hook personnalisé doit être utilisée au plus haut niveau du composant

---

## II - Extraction de logique avec un hook

Ici, on as coder un composant permettant de suivre la position du curseur de la souris. 

```javascript
import { useEffect, useState } from "react";

export default function App() {
  const [x, setX] = useState(0);
  const [y, setY] = useState(0);

  useEffect(() => {
    function update(e) {
      setX((x) => e.pageX);
      setY((y) => e.pageY);
    }
    window.addEventListener("mousemove", update);
    return () => window.removeEventListener("mousemove", update);
  }, []);

  return (
    <main className="flex min-h-screen items-center bg-slate-100 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        <p>x : {x}</p>
        <p>y: {y}</p>
      </div>
    </main>
  );
}
```

On souhaite récupérer la logique pour ensuite pouvoir la réutiliser dans d'autre composants.

On viens créer un  nouveau folder `hooks`. Celui ci contiendras ensuite tous nos hooks personnalisés.
On viens ensuite créer un nouveau fichier `useTrackMouse.js` 

**Systématiquement, on utiliseras `use` en début du nom de fichier.**

Dans ce fichier, on viendras créer une nouvelle fonction que l'on vient exporter, et on viendras copier la partie logique du composant :

```javascript
//src/hooks/useTrackMouse.js
import { useEffect, useState } from "react";

export function useTrackMouse() {
  const [x, setX] = useState(0);
  const [y, setY] = useState(0);

  useEffect(() => {
    function update(e) {
      setX((x) => e.pageX);
      setY((y) => e.pageY);
    }
    window.addEventListener("mousemove", update);
    return () => window.removeEventListener("mousemove", update);
  }, []);
 
 return [x, y]; 
}
```

On viens ensuite importer notre hook personnalisé dans le composant d'origine :

```javascript
import { useTrackMouse } from "./hooks/useTrackMouse";

export default function App() {

  //utilisation du hook personnalisé
  const [x, y] = useTrackMouse();
  
  return (
    <main className="flex min-h-screen items-center bg-slate-100 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        <p>x : {x}</p>
        <p>y: {y}</p>
      </div>
    </main>
  );
}
```

Si on vient utiliser ce hook dans d'autre composant, chacun sera isolé. Les `useState` seront unique au composant.

Avec cette fonctionnalité on gagne en lisibilité et en réutilisation de logique.

---

## III - Utilisation d'un hook avec fetch()

On pourras utiliser ce mécanisme de hook personnalisé pour effectuer des call HTTP.

De base, on a ce code ci pour réaliser des call vers un serveur et obtenir des données stocké dans celui ci : 

```javascript
export default function App() {
  const [recipes, setRecipes] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    async function fetchRecipes() {
      try {
        const response = await fetch("https://restapi.fr/api/recipess");
        if (response.ok) {
          const newRecipes = await response.json();
          setRecipes(Array.isArray(newRecipes) ? newRecipes : [newRecipes]);
        } else {
          setError("Error");
        }
      } catch (e) {
        setError("Error : ", e);
      } finally {
        setLoading(false);
      }
    }
    fetchRecipes();
  }, []);

  return (
    <main className="flex min-h-screen items-center bg-slate-100 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        {loading ? (
          <p>Chargement</p>
        ) : (
          <ul>
            {recipes.map((recipe) => (
              <li key={recipe._id}>{recipe.title}</li>
            ))}
          </ul>
        )}
      </div>
    </main>
  );
```

On pourras venir créer un hook personnalisé afin de pouvoir faire des call de manière simplifié en une seule ligne de code.

On viens créer un nouveau fichier dans le folder `hooks` de notre projet. On viens appeler ce fichier `useFetchRecipes.js`

```javascript
//src/hooks/useFetchRecipes.js

import { useState, useEffect } from "react";

export function useFetchRecipes() {
  const [recipes, setRecipes] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchRecipes() {
      try {
        const response = await fetch("https://restapi.fr/api/recipess");
        if (response.ok) {
          const newRecipes = await response.json();
          setRecipes(Array.isArray(newRecipes) ? newRecipes : [newRecipes]);
        } else {
          setError("Error");
        }
      } catch (e) {
        setError("Error : ", e);
      } finally {
        setLoading(false);
      }
    }
    fetchRecipes();
  }, []);

  return {
    recipes,
    loading,
    error,
  };
}
```

On viens ensuite appeler notre hook dans le composant ayant besoin des données du serveur :

```javascript
import { useFetchRecipes } from "./hooks/useFetchRecipes";

export default function App() {
  // on vient déconstruire le retour du hook perso
  const { recipes, loading, error } = useFetchRecipes();

  return (
    <main className="flex min-h-screen items-center bg-slate-100 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        {loading ? (
          <p>Chargement</p>
        ) : (
          <ul>
            {recipes.map((recipe) => (
              <li key={recipe._id}>{recipe.title}</li>
            ))}
          </ul>
        )}
        {error && <p>{error}</p>}
      </div>
    </main>
  );
}
```

---

## IV - Rendre un hook générique pour le réutiliser

Afin de rendre le hook précédent plus utile, il serait judicieux de le rendre générique afin de pouvoir le réutiliser dans d'autre composants.

On souhaite rendre le hook de fetch générique.

On commence par rendre le nom du hook plus générique : `useFetchData()`

```javascript 
import { useState, useEffect } from "react";

export function useFetchData(url) {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        if (response.ok) {
          const fetchedData = await response.json();
          setData(Array.isArray(fetchedData) ? fetchedData : [fetchedData]);
        } else {
          setError("Error");
        }
      } catch (e) {
        setError("Error : ", e);
      } finally {
        setLoading(false);
      }
    }
    fetchData;
  }, []);

  return {
    data,
    loading,
    error,
  };
}
```

On viens ensuite adapter le composant qui vient fetch la data 

```javascript 
import { useFetchData } from "./hooks/useFetchData";

export default function App() {
  //on viens renommer data en recipes
  const {
    data: recipes,
    loading,
    error,
  } = useFetchData("https://restapi.fr/api/recipess");

  return (
    <main className="flex min-h-screen items-center bg-slate-100 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        {loading ? (
          <p>Chargement</p>
        ) : (
          <ul>
            {recipes.map((recipe) => (
              <li key={recipe._id}>{recipe.title}</li>
            ))}
          </ul>
        )}
        {error && <p>{error}</p>}
      </div>
    </main>
  );
}
```


---
