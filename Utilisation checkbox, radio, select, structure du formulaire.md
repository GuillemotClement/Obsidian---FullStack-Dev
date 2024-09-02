---
created: 2024-09-02T16:31:00
tags:
  - Formulaire
  - React
---
---
## Checkbox

Avec les checkbox, si la case est coché, la valeur retourné dans l'objet du formulaire sera `true`.

Avec `register`, on ajoute une clé correspondant à la case.

```javascript
<div className="flex flex-col">
	<label htmlFor="happy">
	  Content ?
	  <input {...register("happy")} type="checkbox" id="happy" />
	</label>
</div>
```

## Radio

Pour lier les bouton, on utiliseras le `register` en leur ajoutant le même nom. De cette manière, il ne sera possible que d'en sélectionner un.

```javascript
<div className="flex flex-col">
	<label htmlFor="sexe">Sexe</label>
	<div className="">
	  <label htmlFor="man">Homme</label>
	  <input {...register('gender')} type="radio" name="man" id="man" />
	</div>
	<div className="">
	  <label htmlFor="woman">Femme</label>
	  <input {...register('gender')} type="radio" name="woman" id="woman" />
	</div>
</div>
```

## Select

```javascript
<div className="flex flex-col">
	<label htmlFor="sign">
	  Signe astrologique
	  <select id="sign" {...register("sign")}>
		<option value="" disabled>
		  Selectionner un signe
		</option>
		<option value="fish">Poisson</option>
		<option value="aquarius">Verseau</option>
	  </select>
	</label>
  </div>
```

On viendras ajouter une valeur par défaut vide pour afficher `Selectionner un signe` pour améliorer l'utilisation du formulaire
```javascript 
  const {
    register,
    handleSubmit,
    getValues,
    formState: { errors },
  } = useForm({
    defaultValues: {
      sign: "",
    },
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
```

## Modifier la structure du formulaire

On pourras modifier la structure du formulaire afin d'améliorer la maintenabilité du code.

Par exemple, on pourras stocker des données qui sont optionel dans une clé `other` dans le tableau du formulaire.

Pour cela, on viens déclarer la clé dans le tableau des valeur par défaut, et on ajoute un nouvel objet avec les input que l'on souhaite.
On viens ensuite faire référence à cette structure dans le register.

```javascript 
  const {
    register,
    handleSubmit,
    getValues,
    formState: { errors },
  } = useForm({
    defaultValues: {
      gender: "man",
      //on créer la clé other et on place la clé des input
      other: {
        sign: "",
        happy: "",
      },
    },
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });

//on viens faire référence dans l'input
<select id="sign" {...register("other.sign")}>
<option value="" disabled>
  Selectionner un signe
</option>
<option value="fish">Poisson</option>
<option value="aquarius">Verseau</option>
</select>
```
