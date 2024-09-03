---
created: 
tags:
  - Formulaire
  - React
---
---
```table-of-contents
```
## trigger()

Cette méthode permet de déclencher la validation d'un champ.

PAr exemple, on as un formulaire qui utilise le mode de validation `onSubmit`. On souhaite modifier ce mode uniquement pour un champ du formulaire.
Pour réaliser cela, on pourras utiliser cette méthode

On viens récupérer cette méthode depuis le `useForm` 

```javascript
  const {
    register,
    handleSubmit,
	trigger
  } = useForm({
    defaultValues,
});
```

On viens ensuite l'utiliser dans le tableau d'option de `register` sur un input.

```javascript
<input type="text" {...register('name', {
  onBlur(){
	trigger('name')
  }
})} />
```
## setFocus()

Cette méthode permet de retourner sur le focus sur un champ en particulier.

On commence par venir la récupéré depuis le `useForm`. 

```javascript
  const {
    register,
    handleSubmit,
    getValues,
    reset,
    setError,
    clearErrors,
    setFocus,
    formState: { errors, isSubmitting },
  } = useForm({
    defaultValues,
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
});
```

Une fois récupéré, on pourras venir l'invoquer. 

On peut lui passer en paramètre le nom d'un champ du formulaire.

### Focus sur le champ en erreur

On pourras utiliser cette méthode pour mettre le focus sur un input qui n'est pas valider :

```javascript
  async function submit(values) {
    try {
      clearErrors();
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
      setError('name',{ type: 'wrongName', message: e.message})
      setFocus('name');
      console.log("erreur", e);
    }
  }
```

On peut utiliser une autre façon en passant un troisième paramètres à la fonction `setError` avec l'option `shouldFocus`

```javascript
} catch (e) {
      setError('name',{ type: 'wrongName', message: e.message}, {shouldFocus: true})
      setFocus('name');
```

## Afficher toutes les erreurs 

Parfois, il y a plusieurs erreurs pour un champ, et on souhaite venir les afficher.

Par défaut, on n'affiche qu'un seul message d'erreur. Il sera possible de modifier ce comportement en modifiant les option de `useForm`

```javascript 
  const {
    register,
    handleSubmit,
  } = useForm({
    defaultValues,
    //on modifie le comportement 
    criteriaMode: 'all'
  });
```

Dans ce code, on as modifié le comportement pour afficher tous les messages d'erreurs.

On viens ensuite modifier le code du composant pour afficher tous les messages d'erreurs

```javascript
{errors?.name && (
  <ul>
	{ Object.keys(errors.name.types).map(err => (
	  <li key={err}>{errors.name.types[err]}</li>
	))}
  </ul>
)}
```
