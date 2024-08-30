---
created: 2024-08-27T18:48
updated: 2024-08-30T12:39
---
---
```table-of-contents
```
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

[[handleSubmit()]]

### getValues

Permet de récupérer les valeurs actuel du formulaire pour le rendu du composant

## Récupération des champs 

On viens commence par venir récupérer les fonctions `register`, `handleSubmit`

```javascript
const { register, handleSubmit } = useForm();
```

## submit()

Par convention, on viendras créer une fonction submit pour la gestion de la soumission du formulaire.
On passeras cette fonction à la méthode `handleSubmit()`

On vient ensuite préparer une fonction pour gérer la soumission du formulaire. 
Dans cette fonction, on passe en paramètres les valeurs du formulaire.

Cette fonction ne sera exécuté que si le formulaire est validé.

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
On pourras venir utiliser des methodes de cet objet afin de voir les erreur du formulairem si les input on ete cliquer, etc :
`dirtyFields` : les input qui ont ete touche
- `errors` : retourne un objet avec toutes les erreurs dans les input avec leur cle
- `isDirty` : pour savoir si le formulaire a ete touche
- `isSubmitSuccessful` : pour savoir si la soumission du formulaire s'est bien derouler
- `issubmitted` : savoir si on as soumis le formulaire
- `isSubmitting` : permet de savoir si on est en train de soumettre
- `isValid` : permet de savoir si le formulaire est valide
- `submitCount` : permet de savoir combien de fois le formulaire a ete soumis


### Affichage d'une erreur

On viens dans le retour du composant venir afficher si il y a une erreur dans le input.

L'affichage du message se fera une fois le formulaire valider.

On viens déconstruire `formState`, puis on récupère la clé `errors`. On viens ensuite vérifier si il y a une valeur dans cette propriété, et si oui, alors on viens afficher un message :

```javascript
export default function App() {
  const {
    register,
    handleSubmit,
    getValues,
    //on déconstruit formState pour récupérer uniquement la clé errors
    formState: { errors },
  } = useForm({
    defaultValues: {
      //on passe 'Jean' en valeur par défaut au champ name
      name: "",
    },
  });

  //fonction pour la gestion de la soumission
  function submit(values) {
    console.log(values);
  }

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
              {...register("name", {
              //la valeur doit faire au moins 5 caractères
                minLength: 5,
              })}
            />
            {/*Affichage du message d'erreur */}
            //on utilise le ? pour eviter uyn bug si pas de valeur
            {errors?.name && <p>Il y a une fucking erreur</p>}
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


### Préciser un message d'erreur personnalisé

On pourras venir préciser un message personnalisé pour chaque élément que l'on vérifie. Par exemple, ici on ajoute un message personnalisé dans le cas ou l'input ne contient pas au moins 2caractères.

Lorsque l'on vient ajouter un message personnalisé, on pourras directement venir l'utiliser dans le formulaire :

```javascript

<label htmlFor="name">Name</label>
<input
type="text"
className="mt-2 rounded-lg border-2"
id="name"
{...register("name", {
	//on passe un objet, et un clé message
	minLength: {
	  value: 2,
	  message: "Trop court",
	},
})}
/>
//on viens afficher le message d'erreur si l'input ne respect pas 
{errors?.name && <p>{errors.name.message}</p>}
 ```

### Input required

On pourras utiliser `required` pour afficher un message dans le cas ou l'utilisateur n'as pas remplis un input nécessaire :

```javascript
<label htmlFor="name">Name</label>
<input
type="text"
className="mt-2 rounded-lg border-2"
id="name"
{...register("name", {
	//on passe un objet, et un clé message
	minLength: {
	  value: 2,
	  message: "Trop court",
	},
	required: {
		value: true,
		message: "Le champs doit être remplis"
	}
})}
/>
//on viens afficher le message d'erreur si l'input ne respect pas 
{errors?.name && <p>{errors.name.message}</p>}
```

### Création d'une fonction de validation

On viens ajouter une clé `validate` dans le `register` de l'input.  On viens passer directement une fonction 

Lorsque la fonction `validate()` est invoquée, on récupère la valeur du champs en paramètre. A partir de la, on vient réaliser des vérifications.

Pour que le test passe, on viens simplement retourner `true`

```javascript
{...register("name", {
	minLength: {
	  value: 2,
	  message: "Trop court",
	},
	validate(value) {
	  if (value === "Jean") {
			return true;
	  }else{
			return false;
	  }
	},
})}
```

### Récupérer la valeur d'un autre input

Cette fonctionnalité est utile dans le cas ou l'on souhaite faire une confirmation de mot de passe pour une inscription d'un nouvel utilisateur.

Pour cela on viendras utiliser la fonction `getValues()`, ou l'on indique le nom du champ que l'on souhaite en paramètre.
On viens ensuite comparer les deux valeurs

```javascript
{...register("name", 
	{ minLength: {
		value: 2, 
		message: "Trop court", 
	}, 
	validate(value) { 
		getValue("confirm);
		if (value === "Jean") {
			return true;
		}else{ 
			return false; 
		} 
	}, 
})}
```

### valueAsNumber

Cette clé placé sur `register` permet de convertir la saisis d'un utilisateur en number.

Par défaut, le formulaire ne retourne que des string.

```javascript 
<input
  type="number"
  className="mt-2 rounded-lg border-2"
  id="age"
  {...register("name", {
	valueAsNumber: true,
  })}
/>
```

### valueAsDate

De la même manière, on pourras utiliser cette clé pour convertir la valeur en format `Date`

```javascript
<input
  type="number"
  className="mt-2 rounded-lg border-2"
  id="age"
  {...register("name", {
   valueAsDate: true,
  })}
/>
```

### setValueAs

Permet d'utiliser une fonction qui va prendre la valeur, et on pourras retourner ce que l'on souhaite :

```javascript
<input
  type="number"
  className="mt-2 rounded-lg border-2"
  id="age"
  {...register("name", {
	setValueAs(x) {
	  return "Salut";
	},
  })}
/>
```

Dans l'exemple, il considère que la valeur de `x` est `Salut`.

### onBlur

Permet de définir des fonction de callback pour cet effet. 

Par exemple, dans le cas ou l'on souhaite faire un effet particulier pour le `onBlur`

```javascript
<input

              type="number"

              className="mt-2 rounded-lg border-2"

              id="age"

              {...register("name", {

                onBlur(e) {

                  console.log("Blur");

                },

              })}

            />
```

Ici, on déclenche l'effet lorsque l'on clique en dehors du formulaire.

### onChange

De la même façon, on pourras définir une fonction de rappel lorsque l'on viens saisir de la donnée dans le input 

```javascript 
<input

              type="number"

              className="mt-2 rounded-lg border-2"

              id="age"

              {...register("name", {

                onChange(e) {

                  console.log("Change");

                },

              })}

            />
```

Ici, on viens déclencher la fonction lorsqu'on vient saisir de la données dans le input.