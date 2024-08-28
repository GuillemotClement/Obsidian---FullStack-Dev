# Gestion de formulaire

Une gestion de formulaire englobe plusieurs notions :

- UI : ce que voit l'utilisateur, aspect design
- UX : utilisation du formulaire, intuitivité, fluidité
- Validation des champs : synchrone ou asynchrone (vérification directement, ou bien depuis le serveur)
-  Ajout de champs dynamique (ajout d'un bouton selon besoin de l'user)
- Gestion de la soumission (validation, vérification des données)
- Gestion des erreurs
- Gestion d'état : (user à commencé à écrire dans un champ, tentative de soumission, quels infos stocké dans le formulaire )
- Structure : tableau, objet, etc
- Gestion des évènements

Pour la gestion de tous cela, on viens utiliser deux librairies :

- React-hook-form (https://react-hook-form.com/) : c'est la librairie de référence pour la gestion des formulaires. C'est la librairie la plus moderne et performante pour gérer les formulaire. Elle est basée sur les hooks et a une stratégie d'optimisation des rendus performantes.
- Yup (https://www.npmjs.com/package/yup) : permet de mettre en place un mécanisme de validation de données soumis dans le formulaire.

## React-hook-form

Site officiel : https://react-hook-form.com/
### Installation 

Pour utiliser la librairie, on viens l'installer dans le projet.

`npm install react-hook-form`

## Yup

### Installation 

Pour l'installation de la libraire, on viens lancer la commande :

`npm install @hookform/resolvers yup`


## II - Création d'un formulaire

[[Création de formulaire]]

