---
created: 
tags:
  - React
  - ReactRouter
---
---
```table-of-contents
```
# React-Router

C'est une librairie qui permet de mettre en place un système de routing dans une application React.

Pour mettre en place le système de routing, on pourras choisir d'utiliser la librairie React-Router, ou bien d'utiliser le framework Next JS.

React-Router est une solution plus flexible, qui permet de l'adapter à n'importe quel type d'application React.

## Routeur côté client vs Routeur côté serveur

### Côté serveur

C'est la façon basique pour une application serveur. On clique sur un lien sur une page, et cela envoie une requête HTTP au serveur. 
Celle ci est intercepté, et selon l'URL, le serveur génère et retourne la page correspondante.

La réponse est ensuite récupéré par le navigateur, et cela entraîne le rechargement complet de la page.

### Côté client

Dans le cadre d'une SPA, on ne peut pas se permettre de recharger l'application pour changer de page. On vient donc mettre en place un routing côté client.

L'utilisateur clique sur un client, le lien est ensuite intercepter par React et React utilise la librairie `React-Router` pour générer le composant.
Etant donné que l'on ne passe pas par le serveur, il n'y a pas besoin de recharger l'application.