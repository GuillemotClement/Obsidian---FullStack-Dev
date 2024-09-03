---
created: 
tags:
  - React
  - FonctionnalitéConcurrentes
---
---
## Concurrence

La notion de concurrence est arrivée avec React 18. Il pourras mettre en pause la construction des composants pour améliorer les performances.
Cela permet une gestion de plusieurs versions en simultané d'un arbre de composant.

La concurrence permet que plusieurs tâches puissent se chevaucher et être traitées suivant leurs priorités respectives.

## Suspense 

Le composant natif `Suspense` permet d'afficher un élément React en attendant que ses composants enfants aient terminé de charger.

```javascript 
<Suspense fallback={<Chargement />}>
  <UnComposant />
</Suspense>
```

Dans l'exemple, le composant `Suspence` affichera le composant `Chargement` tant que le composant `UnComposant` n'est pas prêt à être rendu.

`Suspence` permet également de charger un composant de manière `lazy`.

[[Composant Suspense]]
