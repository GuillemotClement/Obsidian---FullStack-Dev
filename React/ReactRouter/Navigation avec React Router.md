---
created: 
tags:
  - React
  - ReactRouter
---
---
```table-of-contents
```
# React-Router

C'est une librairie qui permet de mettre en place un système de routing dans une application React.

Pour mettre en place le système de routing, on pourras choisir d'utiliser la librairie React-Router, ou bien d'utiliser le framework Next JS.

React-Router est une solution plus flexible, qui permet de l'adapter à n'importe quel type d'application React.

## Routeur côté client vs Routeur côté serveur

### Côté serveur

C'est la façon basique pour une application serveur. On clique sur un lien sur une page, et cela envoie une requête HTTP au serveur. 
Celle ci est intercepté, et selon l'URL, le serveur génère et retourne la page correspondante.

La réponse est ensuite récupéré par le navigateur, et cela entraîne le rechargement complet de la page.

### Côté client

Dans le cadre d'une SPA, on ne peut pas se permettre de recharger l'application pour changer de page. On vient donc mettre en place un routing côté client.

L'utilisateur clique sur un client, le lien est ensuite intercepter par React et React utilise la librairie `React-Router` pour générer le composant.
Etant donné que l'on ne passe pas par le serveur, il n'y a pas besoin de recharger l'application.

Lorsque `React-Router` intercepte le lien, on aura la possibilité de récupérer de la données depuis le serveur. Le serveur sera utilisé uniquement pour récupérer de la données. 

## Installation de la librairie 

https://reactrouter.com/en/main

Pour pouvoir utiliser la librairie, il faut commence par venir l'installer :

`npm i react-router-dom`
``

# Système de navigation de React-Router

### Création des pages

Dans un premier temps, on viens créer un nouveau folder `src/pages`. 

Dans l'exemple, on viens créer deux nouveau folder `pages/homepage` et `pages/profil`. Chaque nouveau folder correspond à une page de l'application.

![[Pasted image 20240903162221.png]]

### Déclaration du système de routing

Pour la mise en place, on commence par déclarer le système de routing dans le fichier `main.jsx`. On commence par venir provide le routeur.
On viens également spécifier le router
On viens utiliser `ReactProvider` fournis par la librairie :

```javascript
createRoot(document.getElementById("root")).render(
  <StrictMode>
    <RouterProvider router={router}></RouterProvider>
  </StrictMode>,
);
```

On viens ensuite créer le router. On viens le créer dans un nouveau fichier `src/router.jsx`. C'est dans ce fichier que l'on vient créer la carte des routes de l'application.
On viens utiliser la méthode `createBrowserRouter`.

On  viens lui passer un tableau qui correspond à l'ensemble des routes de l'application. Dans ce tableau, on viens ajouter des objets, et chaque objet correspond à une instance de route.

Sur chaque route, on viens spécifier une url et un composant.

```javascript
import { createBrowserRouter } from "react-router-dom";
import App from "./App";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
  },
]);
```

On viens ensuite importer le router dans le fichier `main.jsx` et pouvoir l'utiliser dans le `RouterProvider`

On viendras systématiquement déclarer la route correspondant au `/` correspond à la page d'accueil.

On viendras utiliser la clé `children` afin de spécifier des routes enfants, c'est à dire, qui font partie de la page.
```javascript
//router.jsx
import { createBrowserRouter } from "react-router-dom";
import App from "./App";
import Homepage from "./pages/Homepage/Homepage";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      {
        path: "/",
        element: <Homepage />,
      },
    ],
  },
]);
```

On viens ensuite utiliser le composant `<Outlet />` pour indiquer ou placer ce composant enfant.

```javascript
//App.jsx
import Header from "./components/Header";
import { Outlet } from "react-router-dom";
export default function App() {
  return (
    <main className="flex min-h-screen flex-col">
      <Header />
      <Outlet />
    </main>
  );
}
```

`React-Router` vient remplacer `Outlet` par le composant indiqué dans la propriété `children` 

On viens ensuite ajouter une nouvelle route pour accéder à une deuxième page :

```javascript
//router.jsx
import { createBrowserRouter } from "react-router-dom";
import App from "./App";
import Homepage from "./pages/Homepage/Homepage";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      {
        path: "/",
        element: <Homepage />,
      },
       {
        path: "/profil",
        element: <Profil />,
      },
    ],
  },
]);
```

### Naviguer entre les pages

Pour accéder aux différentes pages, on viens utiliser le composannt `<Link>`.  On viendras y placer du texte qui sera affiché sur la page, et une clé `to` pour indiquer le path que l'on souhaite accéder.

```javascript
export default function Header() {
  return (
    <div className="flex h-11 items-center justify-between border-b px-4 shadow-lg">
      <div className="">
        <p>logo</p>
      </div>
      <ul className="flex gap-x-3">
        <Link to="/">Accueil</Link>
        <Link to="/profil">Profil</Link>
      </ul>
    </div>
  );
}
```

Dans ce composant `Header`, on créer un menu de navigation simple qui permet d'accéder au deux pages que l'on as créer dans le `router.jsx`

# Option index et caseSensitive et gestion des erreurs

## Option index

Pour les route `children`, on pourras utiliser une notation alternative au lieu d'utiliser le `/` 

On viendras utiliser passer l'option `index` à `true`. C'est l'élément avec cet option qui sera chargé par défaut 

```javascript 
export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: [
      {
        index: true,
        element: <Homepage />,
      },
      {
        path: "/profil",
        element: <Profil />,
      },
    ],
  },
]);
```

Cet option n'est utilisable que dans le cas ou l'on se situe dans une clé `children`.

## Gestion d'erreur 

Dans le cas ou l'on vient créer un lien qui vers une path qui n'est pas déclarer dans le fichier `router.jsx`, on obtient une page d'erreur.

On pourras améliorer l'ux en précisant un `errorElement` dans le `Router`, et on pourras venir préciser un composant. 
Ce composant sera utiliser dans le cas le path n'existe pas.

### Configurer une page d'erreur 

On viendras au plus haut niveau du `Router`, ajouter une novelle clé `errorElement`. On viendras préciser un composant qui sera utilisé.

On pourras également l'ajouter dans des niveau plus profond,

````javascript
export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    errorElement: <ErrorPage />,
    children: [
      {
        index: true,
        element: <Homepage />,
      },
      {
        path: "/profil",
        element: <Profil />,
      },
    ],
  },
]);
````` 

On viendras créer le composant dans `src/pages/ErrorPage`. Dans le cas ou la path n'est pas trouvé dans le fichier `router.jsx`, alors c'est ce composant qui sera affiché.

### Récupérer le code d'erreur 

Il sera possible de venir récupérer le code d'erreur depuis le composant qui gère la page d'erreur en utilisant un hook fournit par la librairie.

Ce hook viens retourner l'objet d'erreur qui à déclencher l'effet de charger ce composant en particulier.

```javascript
import { useRouteError } from "react-router-dom";

export default function ErrorPage() {
  const error = useRouteError();
  return (
    <div className="">
      <h2>
        {error.status} : {error.data}
      </h2>
    </div>
  );
}
```

Dans ce code, on affiche le code erreur et le message d'erreur.

## Gestion des majuscules

Cette option permet de préciser que l'on souhaite prendre en compte les majuscules.

Cela sera pris en compte par la navigation via les liens.

Pour activer cette option, on viens ajouter la clé dans le fichier `router.jsx`

```javascript
export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    errorElement: <ErrorPage />,
    children: [
      {
        index: true,
        element: <Homepage />,
      },
      {
        path: "/profil",
        caseSensitive: true,
        element: <Profil />,
      },
    ],
  },
]);
```

# useMatch, Link et navLink
