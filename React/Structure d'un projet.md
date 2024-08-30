[[React/React]]

----

# Structure d'un projet

Afin de garder une bonne lisibilité du code dans un projet, il est important de respecter au maximum une structure facilement maintenable.

En agrandissant, une application React va grossir en terme de composant, et il est donc important de garder une bonne structure.

## Méthodologie

Dans le dossier `src` du projet, on vient créer plusieurs folders :

- `pages`: dans ce folder, on retrouve les composants principaux, par exemple `Homepage`
- `components`: on viendras placer dans ce folder, les composants utilisé partout dans l'application tel que `Header.jsx`, et `Footer.jsx`.

On peut également venir créer des sous-dossier pour contenir le fichier composant et le fichier module scss. 

### Mise en pratique 

Ici, on retrouve l'exemple `CookChef` réalisé pendant la formation Dyma. 

On viens placer dans le dossier `src/pages/Homepage` le fichier `Content.jsx` & `Content.modules.scss` qui est le composant principal qui contient la homepage de notre application.
On ajoute également le fichier `Recipe.jsx` avec son module scss car ce composant est utilisé uniquement dans le composant `Content` .

Dans le folder `components`, on conserve les fichiers `Footer.jsx` et `Header.jsx` que l'on vient ajouter dans des sous-dossier qui regroupe le composant et son module scss. Par exemple, on retrouve un folder `src/components/Header` qui contient à la fois le fichier `Header.jsx` et `Header.module.scss`

Dans le folder `Header`, on viens ajouter un nouveau folder `components` car on a ajouter un autre composant `MenuMobile` dans le header qui est chargé du menu mobile. On viendras ensuite rassembler le composant et son scss dans un sous dossier.

![[Pasted image 20240826124526.png]]