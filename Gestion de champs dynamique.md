---
created: 
tags:
  - Formulaire
  - React
---
---

Pour mettre en place des champs dynamique, on commence par récupérer une nouvelle méthode depuis `useForm`.

```javascript
  const {
    register,
    handleSubmit,
    control,
  } = useForm({
    defaultValues,
    criteriaMode: 'all'
    resolver: yupResolver(yupSchema),
  });
```

Cette méthode permet d'ajouter des champs dans le useForm

### Préparation du formulaire

On commence par préparer le formulaire. Ici on ajoute un nouveau label contenant du texte et un bouton.
Lors du clique sur un bouton, cela permet d'ajouter un nouvel élément :

Pour éviter que ce bouton déclenche la validation du formulaire, on viens modifier son type.

On viens ensuite ajouter un event sur le bouton permettant de récupérer le click qui viendras déclencher une fonction permettant d'ajouter une nouvelle activité

```javascript
<div className="">
//on créer un label avec un bouton
<label htmlFor="activity">
  <span>Activités</span>
  <button type="button" onClick={addActivity}>+</button>
</label>
</div>
```

### Ajout de la fonction d'ajout

Une fois le click catcher, on vient déclarer la fonction. Celle ci à pour but d'ajouter un nouveau champ dans le tableau d'activité.

On viens préparer ce tableau dans le tableau de valeur par défaut :

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
    activities: [],
  };
```

On viens ensuite récupérer la fonction `useFieldArray` depuis le hook `useForm`. Cette méthode retourne des éléments permettant d'ajouter des champs dans le tableau, de retirer, de parcourir, etc

On viens lui passer en paramètre un objet.

```javascript
  const {fields, append, remove} = useFieldArray({
    //on indique le champ concerné
    name: 'activities',
    //on lui passe également le contrôle -> permet d'ajouter des champs dans le useFrm
    control
  });
```


On obtient ainsi l'accès à un objet contenant des méthodes permettant de manipuler les champs.
On récupéré directement des les méthodes qui nous intéresse

On viens ensuite préparer la fonction addActivity

```javascript
  function addActivity(){
    //on viens ajouter un nouveau champ
    //on lui passe un objet
    append({
      value: ''
    })
  }
```

On prépare ensuite dans le formulaire 

```javascript 
<div className="">
//on créer un label avec un bouton
<label htmlFor="activity">
  <span>Activités</span>
  <button type="button" onClick={addActivity}>+</button>
</label>
<ul>
{ fields.map( activity, i) => (
  <li key={activy.id}>
	<input type="text" {...register(`activities[${ i }].value`)/>
	<button>-</button>
  </li>
))}
</ul>
</div>
```
