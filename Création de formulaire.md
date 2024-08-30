La librairie React-hook-form à créer un hook qui permet une gestion de formulaire simplifié. Avec son hook, on pourras facilement venir gérer le formulaire.

Lorsque l'on vient utiliser une balise `label` avec React, on viendras utiliser l'attribut `htmlFor=""` pour venir binder un  label avec un input. 

### Création du formulaire

On viens créer un formulaire basique qui permet de récupérer un nom d'utilisation :

```javascript 
<div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
	<form>
	  <div className="flex flex-col">
		<label htmlFor="name">Name</label>
		<input type="text" className="mt-2 rounded-lg border-2" id="name" />
	  </div>
	  <button className="mt-5 rounded-lg bg-blue-500 px-3 py-1 text-white shadow-lg">
		Valider
	  </button>
	</form>
</div>
```
![[Pasted image 20240827190305.png]]

Avec ce formulaire, lorsque l'on vient cliquer sur le bouton cela vient rafraichir la page, ce qui est le comportement par défaut.

## useForm()

C'est le hook le plus important de la librairie. Celui ci va permettre de contrôler l'ensemble du formulaire.

On viens l'importer depuis `react-hook-form`, puis on viendras l'utiliser dans notre composant React.

```javascript
import { useForm } from "react-hook-form";

export default function App(){

	useForm();

}
```

La fonction `useForm()` permet de contrôler l'ensemble du formulaire. Il suffit de l'invoquer.
Cette fonction retourne un objet qui permet de connecter le formulaire avec la partie template

Chacune des propriétés de l'objet aura un rôle spécifique.

### register

Permet d'enregistrer un input à l'intérieur du formulaire.
Ici, on as l'input name que l'on souhaite lier au formulaire.
### handleSubmit

Cette propriété permet de configurer la méthode qui sera appelé lorsque l'on viendras cliquer sur le bouton de validation.
Cela permet de récupérer les valeur stocké dans les formulaires.
### getValues

Permet de récupérer les valeurs actuel du formulaire pour le rendu du composant

## Récupération des champs 

On viens commence par venir récupérer les fonctions `register`, `handleSubmit`

```javascript
const { register, handleSubmit } = useForm();
```

On vient ensuite préparer une fonction pour gérer la soumission du formulaire. 
Dans cette fonction, on passe en paramètres les valeurs du formulaire.

```javascript
function submit(value){
	console.log(value);
}
```

Pour venir utiliser cette fonction, on viendras binder l'evenement `onSubmit` sur l'élément `<form>`. On passeras la fonction utiliser pour la gestion de la soumission, ici `submit`. 
```javascript
<form onSubmit={handleSubmit(submit)}>
	...
</form>
```

Cela permet de mettre en place des comportements par défaut, tel que le rechargement par défaut de la page qui est retirer.

On vient maintenant connecter le champ au formulaire. 
Pour cela, on viens récupérer le `register` et on vient le déconstruire sur l'input.

```javascript 
<input
  type="text"
  className="mt-2 rounded-lg border-2"
  id="name"
  //permet d'enregistrer l'input pour le recup à la validation du formulaire
  {...register("name")}
/>
```

L'input est maintenant connecter, et on peut venir récupérer la valeur présent dans le input.

On obtient un objet dans `value`, avec en clé que l'on est venus indiqué dans le `register()`.  De cette manière, on pourras ajouter une clé pour chaque input et on les retrouveras dans cet objet. 
Il faut utiliser des clé uniques.

### Recap 

```javascript
//récupération du hook
import { useForm } from "react-hook-form";

export default function App() {
  //récupération des deux méthodes de useForm
  const { register, handleSubmit } = useForm();

  //on vient créer la fonction qui permet la gestion du formulaire
  //values contient les valeurs des inputs
  function submit(values) {
    console.log(values);
  }

  return (
	//on ajoute l'event sur le form et on lui passe la fonction  
	<form onSubmit={handleSubmit(submit)}>
	  <div className="flex flex-col">
		<label htmlFor="name">Name</label>
		<input
		  type="text"
		  id="name"
		  //on enregistre l'input
		  //name étant la clé pour récupérer la valeur dans values
		  {...register("name")}
		/>
	  </div>
	  <button>
		Valider
	  </button>
	</form>
  );
}
```

### Récupérer la valeur du formulaire

Pour récupérer cette valeur, on viens utiliser la méthode `getValue`. On viendras récupérer cette méthode depuis le hook `useForm`.

`const { register, handleSubmit, getValues } = useForm();`

On pourras venir invoquer cette méthode. Dans le cas ou on ne lui passe rien en paramètre, elle viens retourner l'ensemble des valeurs actuel du formulaire.

### watch()

On viens récupérer cette méthode depuis le hook.

`const { register, handleSubmit, getValues, watch } = useForm();`

Cette méthode `watch()`, à partir du moment ou celle ci est invoquer, viens changer le comportement du hook.

A chaque modification de valeur dans un input du formulaire, le composant est reconstruit.
De cette manière, on aura la valeur qui sera récupérer par `getValue()`

```javascript
export default function App() {
  const { register, handleSubmit, getValues, watch } = useForm();
  //on appelle la méthode pour modifier le comportement du hook
  watch();
  
  function submit(values) {
    console.log(values);
  }

  //on utilise la méthode getValues() pour obtenir la valeur du formulaire.
  //a chaque modif d'une valeur, celle ci est affiché
  console.log(getValues());

  return (

    <main className="flex min-h-screen items-center bg-slate-400 py-3">
      <div className="mx-auto flex flex-col justify-center rounded-md bg-white px-6 py-3 shadow-md">
        <form onSubmit={handleSubmit(submit)}>
          <div className="flex flex-col">
            <label htmlFor="name">Name</label>
            <input
              type="text"
              className="mt-2 rounded-lg border-2"
              id="name"
              {...register("name")}
            />
          </div>
          <button className="mt-5 rounded-lg bg-blue-500 px-3 py-1 text-white shadow-lg">
            Valider
          </button>
        </form>
      </div>
    </main>
  );
}
```

On pourras passer à cette méthode le nom d'un champ. Le composant sera reconstruit uniquement si la valeur dans l'input passé est modifié.

## Option de register() & useForm()

On pourras passer un objet de configuration dans le `useForm()`. 

### defaultValues

On pourras le passer en paramètre de l'objet. 

On pourras y indiquer le nom des champs du formulaire et définir une valeur par défaut.

```javascript
const { register, handleSubmit, getValues, watch } = useForm({
    defaultValues: {
      //on passe 'Jean' en valeur par défaut au champ name
      name: "Jean",
    },
  });
```

Ce mécanisme sera très utile dans le cas ou on viens réaliser des mise à jours de quelque chose qui existe déjà.
Par exemple, on as une recette, et on viens préremplir le formulaire avec les différentes données de la recette. De cette manière l'utilisateur pourras venir réaliser des mise à jours de la recette.

L'ajout de valeur par défaut est une bonne pratique. On viendras toujours le réaliser.
Cela permet d'obtenir une vue rapide du contenu du formulaire et on as toujours des valeurs dans les champs.

Dans le cas ou il n'y a pas de valeur, on indique une chaîne vite 

```javascript
const { register, handleSubmit, getValues, watch } = useForm({
    defaultValues: {
      //on passe 'Jean' en valeur par défaut au champ name
      name: "",
    },
  });
  
```

### Paramètre de register

On pourras venir passer des paramètres dans le register. On pourras venir ajouter des éléments de validation basique.
Ce sont les éléments de validation de HTML.

```javascript
<input
  type="text"
  className="mt-2 rounded-lg border-2"
  id="name"
  {...register("name", {
	disabled: true,
  })}
```

On pourras venir les personnalisés.

On retrouve les éléments :
- deeps: permet d'indiquer des dépendances
- disabled: permet de désactiver un champ, l'utilisateur ne pourras plus cliquer sur l'input.
- max, min : lorsque l'on vient manipuler des nombres
- maxLength & minLength : vérifie la longueur de la chaîne de caractère dans l'input. On viens lui passer une valeur.

## Vérifier si il y a une erreur dans le formulaire

Pour cela, on viens récupérer la méthode `formState` depuis le hook. Cette méthode retourne un objet.

On pourras voir si un input à été toucher, si une erreur est présente depuis l'objet retourner par la méthode.

*minute 5 de la vidéo dyma -> options de register() & useForm()*