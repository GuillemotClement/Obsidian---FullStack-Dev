---
created: 2024-09-02T17:09:00
tags:
  - Formulaire
  - React
---
---
```table-of-contents
```
# Gestion de la soumission du formulaire

Lorsque l'on vient soumettre un formulaire, si l'un des champs ne respect pas la validation, alors la fonction [[handleSubmit()]] ne sera pas déclencher.

### Envoie des données du formulaire au serveur

Une fois que les données sont valide, on peut faire les requêtes vers le serveur pour qu'elle soit prise en compte.
On viens créer une fonction asynchrone pour la gestion de ses données.

```javascript 
  //fonction pour la gestion de la soumission
  async function submit(values) {
    try {
      //on prépare la requête avec les données du formulaire
      const response = await fetch("@API", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        //on envoie les valeurs récupérer dans le formulaire
        body: JSON.stringify(values),
      });
      //on vient vérifier que la requête s'est bien déroulée
      if (response.ok) {
        //si ok alors on extrait la réponse du serveur
        const newUser = await response.json();
        console.log(newUser);
      } else {
        console.log("erreur");
      }
    } catch (e) {
      console.log("erreur", e);
    }
  }
```

Dans le cas ou la ressource est bien créer, on affiche dans la console la nouvelle ressource créer en base de donnée.

Pour le mot de passe, il faut prévoir une gestion de hashage de celui ci via le back-end par mesure de sécurité.
C'est la responsabilité de serveur (back-end)

### Réinitialisation des champs

Une fois que la ressource à été envoyer au serveur, et que la ressource à bien été créer, on viens reset les données dans le formulaire.
De cette manière, on indique à l'utilisateur que les données ont bien été soumise.

Pour cette fonctionnalité, on viendras récupérer la fonction `reset()` depuis le hook `useForm`. Celle ci permet de reset les valeurs du formulaire.

On passeras en paramètre de cette fonction, un objet avec les valeurs que l'on appliqueras pour le reset du formulaire.

Etant donné que l'on souhaite mettre les valeurs par défaut, on viens stocker les valeurs par défaut

Dans une constante, on viens stocker les valeurs par défaut :

```javascript 
  const defaultValues = {
    name: "",
    gender: "man",
    age: "",
    password: "",
    confirmPassword: "",
    other: {
      sign: "",
      happy: false,
    },
  };
```

Dans les paramètre du `useForm`, on viens utiliser cette constante pour indiquer les valeurs par défaut du formulaire 

```javascript 
  const {
    register,
    handleSubmit,
    getValues,
    reset,
    formState: { errors },
  } = useForm({
    defaultValues,
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
```

On passe ensuite l'objet des valeurs par défaut dans la méthode `reset()` 

```javascript 
  //fonction pour la gestion de la soumission
  async function submit(values) {
    try {
      //on prépare la requête avec les données du formulaire
      const response = await fetch("@API", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        //on envoie les valeurs récupérer dans le formulaire
        body: JSON.stringify(values),
      });
      //on vient vérifier que la requête s'est bien déroulée
      if (response.ok) {
        //si ok alors on extrait la réponse du serveur
        const newUser = await response.json();
        //une fois l'user créer, on vient reset les valeurs dans le formulaire
        reset(defaultValues);
        console.log(newUser);
      } else {
        console.log("erreur");
      }
    } catch (e) {
      console.log("erreur", e);
    }
  }
```

### Empêcher la double soumission

Pour empêcher l'utilisateur d'envoyer plusieurs fois la même ressource, on viendras rendre inactif le bouton tant que la soumission est en cours.

On viendras récupérer la clé `useSubmitting` du `formState` .  On viens ensuite utiliser cette propriété avec le bouton de validation du formulaire.

```javascript
  const {
    register,
    handleSubmit,
    getValues,
    reset,
    //on récupère la propriété
    formState: { errors, isSubmitting },
  } = useForm({
    defaultValues,
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
 ...

 //on évalue la propriété pour disabled le bouton de validation
 <form>
	 ...
	 <button disabled={isSubmitting}>Valider</button>
</form>

```

### Récupérer le nombre de soumission

On pourras récupérer la nombre de soumission avec la propriété `submitCount`.

De la même façon, on viendras récupérer la propriété depuis le `formState`. On pourras ensuite venir utiliser la propriété dans le composant.

### Gestion d'erreur

Pour gérer les erreurs, il faudras venir les set manuellement. En effet, les erreurs côté serveur ne sont pas pris en compte par React.

Pour cela, on viens récupérer la méthode `setError` depuis le hook `useForm`.  

```javascript
  const {
    register,
    handleSubmit,
    getValues,
    reset,
    setError
    formState: { errors, isSubmitting },
  } = useForm({
    defaultValues,
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
```

On passera en premier paramètre le nom du champ concerné, en second paramètre les options de l'erreur

```javascript
  async function submit(values) {
    try {
      const response = await fetch("@API", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(values),
      });
      if (response.ok) {
        const newUser = await response.json();
        reset(defaultValues);
      } else {
        console.log("erreur");
      }
    } catch (e) {
    //on affiche le message d'erreur si echec
      setError('name',{ type: 'wrongName', message: e.message})
    }
  }
```

### Erreur globale

On pourras également avoir des erreur générique. Dans ce cas, au lieu de préciser un nom de champ, on utilise un nom qui n'existe pas : 

```javascript
  async function submit(values) {
    try {
      const response = await fetch("@API", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(values),
      });
      if (response.ok) {
        const newUser = await response.json();
        reset(defaultValues);
      } else {
        console.log("erreur");
      }
    } catch (e) {
    //on affiche le message d'erreur si echec
      setError('globalError',{ type: 'wrongName', message: e.message})
    }
  }
```

On viens ensuite ajouter dans le composant un nouveau paragraphe pour afficher le message d'erreur à la fin du formulaire :

```javascript 
<form onSubmit={handleSubmit(submit)}>
  ...
  {errors.globalError && <p>{errors.globalError.message</p>}}
  <button
	disabled={isSubmitting}
>
	Valider
  </button>
</form>
```

### Effacer erreur global 

Pour venir effacer une erreur global, il faudras venir utiliser la méthode `clearErrors` depuis le hook `useForm`

```javascript
  const {
    register,
    handleSubmit,
    getValues,
    reset,
    setError,
    clearErrors,
    formState: { errors, isSubmitting },
  } = useForm({
    defaultValues,
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
```
A partir du moment ou l'on vient invoquer cette méthode, cela viens clear toutes les erreurs. On pourras venir passer un champs en particulier.

On pourras venir l'invoquer lorsque l'on viens faire la requête pour nettoyer le formulaire : 

```javascript
  async function submit(values) {
    try {
	  //on vient nettoyer le formulaire lors de l'envoie de celui ci
      clearErrors();
      const response = await fetch("@API", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
 ......
  }
```
