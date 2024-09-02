---
created: 2024-08-30T22:24:00
updated: 
tags:
  - Formulaire
  - React
---
---

```table-of-contents
```

# Yup 

https://github.com/jquense/yup

On pourras utiliser le système de validation de base pour la gestion d'un petit formulaire. Dans le cas ou celui ci deviens gros et difficile à gérer, on pourras venir utiliser la librairie `Yup`.

Cette librairie propose une syntaxe plus élégante et plus rapide.

## Fonctionnement

On viendras importer un certains nombre de type depuis `Yup`, et à partir de la on viendras créer des schémas.

On viens utiliser `object` dans lequel on vient passer un paramètre. Dans celui ci, on viens indiquer le nom des clés et on pourras venir spécifier le type du champs, différentes règles spécifique au champs.


Par exemple : 
```javascript
//on viens importer les types depuis la libraire
import { object, string, number, date, InferType } from 'yup';

//on viens utiliser object
let userSchema = object({
//on indique le rôle des clés et on spécifie le champs, type ..
//ici on vérifie que la clé name est de type texte et est renseigné&
  name: string().required(), 
  age: number().required().positive().integer(),
  email: string().email(),
  website: string().url().nullable(),
  createdOn: date().default(() => new Date()),
});

// parse and assert validity
let user = await userSchema.validate(await fetchUser());

type User = InferType<typeof userSchema>;
/* {
  name: string;
  age: number;
  email?: string | undefined
  website?: string | null | undefined
  createdOn: Date
}*/
```

On pourras ensuite connecter le schéma avec le hook form.

### Récupération des méthodes de Yup

Pour pouvoir utiliser la librairie, on viendras récupérer toutes les méthodes. On utiliseras l'opérateur `*` afin de stocker dans un nouvel objet `yup` toutes les méthodes de la librairie.

L'importation est à réaliser en dehors du composant.

```javascript 
import * as yup from "yup";
```

### Création d'un schéma de validation

On commence par venir créer un nouveau schéma. 
On viens utiliser la méthode `yup.object()` pour venir décrire le contenu du formulaire. On viendras déclarer ce nouveau formulaire dans un objet.

On pourras venir enchaîner les méthodes de validation avec l'opérateur `.` 

```javascript
const yupSchema = yup.object({
	name: yup.string().required().min(2).max(10),
	age: yup.number().min(18),
});
```

Pour l'input `name`, on indique que celui ci est required, qu'il doit avoir une longueur minimum de 2 caractères et une longueur max de 10 caractères.

Pour l'input `age`, on indique que l'input est doit être un nombre, et d'une valeur mini de 18.

### Utilisation du schéma 

Une fois le schéma déclarer, il faut venir utiliser une méthode pour pouvoir l'utiliser sur le formulaire. 
On viens importer le `yupResolver` : 

`import { yupResolver } from "@hookform/resolvers/yup";`

On viens ensuite dans l'objet de configuration de `useForm`, venir préciser le `resolver` 

On viens lui passer en paramètre, le schéma de validation que l'on souhaite utiliser.

```javascript
  const {
    register,
    handleSubmit,
    getValues,
    watch,
    formState: { errors },
  } = useForm({
    defaultValues: {
      name: "",
    },
    resolver: yupResolver(yupSchema),
    mode: "onBlur",
  });
```

Le schéma de validation est maintenant connecter au formulaire.

### Préciser des messages d'erreurs

On pourras directement depuis le schéma de validation préciser des message d'erreurs.

Pour cela, il suffit de passer un paramètre à la fonction de validation.

```javascript
const yupSchema = yup.object({ 
	name: yup.string().required("Le champ est obligatoire").min(2, "La saisis doit être de 2 caractères minimum").max(10), 
	age: yup.number().min(18), 
});
```
### Erreur NaN

Il peut arriver que lorsque l'on soumet un nombre dans un input de type `number`, une erreur `NaN` se produit.
Cela se produit dans le cas ou l'input est vide.

Pour résoudre ce problème, on peut utiliser une méthode `typeError()` et on ajoute un message d'erreur :

```javascript
const yupSchema = yup.object({ 
	name: yup.string().required().min(2).max(10), 
	age: yup.number().min(18).typeError("Saisir un nombre"), 
});
```

### Vérifier si email 

On pourras utiliser la méthode `email()` pour vérifier que la saisis correspond bien à un mail :

```javascript
const yupSchema = yup.object({ 
	mail: yup.string().required().mail(), 
	age: yup.number().min(18).typeError("Saisir un nombre"), 
});
```

### Vérifier si url

On pourras utiliser la méthode `url()` pour vérifier si un input est bien un email :

```javascript
const yupSchema = yup.object({ 
	url: yup.string().required().url("Saisis un url"), 
	age: yup.number().min(18).typeError("Saisir un nombre"), 
});
```

### Input requis

On utilise la méthode `required()` : 

```javascript
const yupSchema = yup.object({ 
	url: yup.string().required().url("Saisis un url"), 
	age: yup.number().min(18).typeError("Saisir un nombre"), 
});
```

## Test asynchrone & croisé

### Système de confirmation de mot de passe

On commence par ajouter les règle de validation des deux input :

```javascript
const yupSchema = yup.object({
    name: yup
      .string()
      .required("Le champ est obligatoire")
      .min(2, "Trop court")
      .max(10, "Trop long"),
    age: yup.number().min(18, "Trop jeune").typeError("Saisir un nombre"),
    password: yup
      .sting()
      .required("Saisir un mot de passe")
      .min("Mot de passe trop court")
      .max("Mot de passe trop long"),
    confirmPassword: yup
      .String()
      .required("Confirmer le mot de passe")
      .oneOf(
        [yup.ref("password"), ""],
        "Les mots de passe ne sont pas identique",
      ),
  });
```

`oneOf` permet de comparer la valeur de deux input. Ici on compare la valeur de l'input `password` avec `confirmPassword`. Dans le cas ou l'une des deux valeurs n'est pas identique, on obtient le message d'erreur indiqué.

`yup.ref()` permet de récupérer une référence à un input du formulaire.

### Fonction de validation personnalisée 

Pour mettre en place des fonctions de validation personnalisée, on viens utiliser la méthode `test()`.
On viens ensuite configurer la méthode dans cette fonction.

En premier paramètre on viens ajouter un nom pour cette validation, en second argument le message d'erreur qui sera retourné dans le cas ou la validation n'est pas passé, et en troisième argument on pourras déclarer une fonction.
Si elle retourne `true` alors la validation est passé.

On pourras utiliser une fonction asynchrone. De cette façon, on pourras venir vérifier qu'une adresse mail est bien présente dans la base de donnée par exemple.

```javascript
const yupSchema = yup.object({
    name: yup
      .string()
      .required("Le champ est obligatoire")
      .min(2, "Trop court")
      .max(10, "Trop long")
      .test("isYes", "Pas de chance", async () => {
        const response = await fetch("https://yesno.wtf/api");
        const result = await response.json();
        return result.answer === "yes";
      }),
  });
```

Dans l'exemple, on utilise une API qui retourne yes ou no. 
Dans le cas ou la réponse est autre que `yes`, on affiche le message d'erreur. La validation à échouée.