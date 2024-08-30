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
- all : 