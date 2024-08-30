Cette propriété permet de configurer la méthode qui sera appelé lorsque l'on viendras cliquer sur le bouton de validation.
Cela permet de récupérer les valeur stocké dans les formulaires.

On viendras placer cette méthode sur le formulaire afin de le connecter :

```javascript
<form onSubmit={handleSubmit(submit)}>
	//code du formulaire
</form>		
```

On viendras passer la fonction `submit()` en paramètre pour utiliser les valeurs du formulaire
## submit()

Par convention, on viendras créer une fonction `submit()` pour la gestion de la soumission du formulaire.
On viendras passer un paramètre `values` qui correspond au valeurs des input du formulaire.
```javascript
function submit(values) {
	console.log(values);
}
```
On passeras cette fonction à la méthode `handleSubmit()`

On vient ensuite préparer une fonction pour gérer la soumission du formulaire. 
Dans cette fonction, on passe en paramètres les valeurs du formulaire.

Cette fonction ne sera exécuté que si le formulaire est validé.
