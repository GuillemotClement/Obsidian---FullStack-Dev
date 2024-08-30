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

On pourras ensuite connecter le shéma avec le hook form.

** arrivé 3' chapitre yup