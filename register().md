---
tags:
  - Formulaire
  - React
created: 2024-08-30T15:55:00
updated:
---
---
```table-of-contents
```

# Register()

Cette méthode permet de connecter un `input` au hook du formulaire.

On viens y indiquer le nom de l'input afin de pouvoir ensuite retrouver la valeur de l'input depuis l'objet du formulaire 
Chaque nom d'input doit être unique dans le formulaire

On pourras venir préciser des options.
## Options de validation de champ

### required 

Rend un champ du formulaire obligatoire.

### maxLength & minLength 

Permet de définir une taille min et max pour la valeur de l'input de type `text`.

### max & min 

Permet de définir une valeur max et min sur un champ de type `number`

### pattern 

Défini une regex pour un champ. 

### validate()

Défini une fonction ou plusieurs fonctions personnalisé de validation

```javascript
//version longue
<input
  {...register("test", {
   validate(value) {
      if (value === '1') {
      return true;
      } else {
        return "Message d'erreur";
      }
    },
  })}
/>

//version raccourcie 
<input
  {...register("test", {
    validate: value => value === '1' || "Message d'erreur"
  })}
/>

//fonction multiple 
<input
  {...register("test1", {
    validate: {
      positive: v => parseInt(v) > 0 || 'Doit être plus grand que 0',
      lessThanTen: v => parseInt(v) < 10 || 'Doit être plus petit que 10',
      checkUrl: async () => await fetch() || "Message d'erreur",
      messages: v => !v && ['test', 'test2']
    }
  })}
/>

```

## Options

### disabled 

Permet de désactiver un champ du formulaire

### valueAsNumber 

Permet de retourner un nombre au lieu d'une chaîne comme valeur du champ.

### valueAsDate 

Permet de retourner une date au lieu d'une chaîne comme valeur du champ

### setValueAs()

Permet de passer une fonction qui transforme la chaîne et la retourne comme valeur.

```javascript
<input
  type="number"
  {...register("test", {
    setValueAs: v => parseInt(v)
  })}
/>
```


### onChange()

Permet de passer une fonction à chaque changement du input

### onBlur()

Permet de passer une fonction invoqué dès que le champ perd le focus
