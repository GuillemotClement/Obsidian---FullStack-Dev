---
created: 2024-08-30T16:05:00
updated: 
tags:
  - Formulaire
  - React
---
---
```table-of-contents
```
# useForm()

## Options 

### mode

Permet de configurer le mode de validation du formulaire. 
- onChange : valider à chaque changement de champ. Impacte la performance
- onBlur : validation à la perte du focus
- onSubmit : valeur par défaut. La validation se fait à la soumission du formulaire
- onTouched : validation lors du premier évènement `blur`, puis à chaque changement
- all : validation sur chaque event `blur` ou `change`. Gros impact sur les performances.

### reValidateMode

Cette option permet de configurer la stratégie de validation pour les champs qui comportent au moins une erreur après qu'un utilisateur est envoyé le formulaire. On pourras utiliser les valeurs suivantes :
- onChange : validation à chaque changement de chaque champ. Impact élevé sur les performances
- onBlur : validation lorsque le champ perd le focus
- onSubmit : validation lors de l'envoi

### defaultValues 

Cette option permet de préciser des valeurs par défaut pour chaque champ enregistré.

La bonne pratique est de définir des valeurs par défaut (qui peuvent être des chaîne de caractère vide ou `null)


