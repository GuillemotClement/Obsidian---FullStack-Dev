# Strutures

## atoms

Dans ce dossier, on retrouve les composants les plus basiques. On retrouve par exemple : 
- Buttons.tsx : Bouton
- Input.tsx : 
- Spinner.tsx
- Checkbox
- Radio
- Link

## molecules

Ce sont des groupes d'atomes relativement simple fonctionnant ensemble comme une unité :
- `SearchBar.tsx` : combine un input et un bouton de recherche
- `FormField.tsx` : label, input et message d'erreur
- `MenuItem.tsx` : icône et texte pour un élément de menu
## organisms

Ce sont des composants plus complexes composé de molécules, et/ou d'atome. Il représente des sections distinct d'une interface :
- `Header.tsx`
- `Footer.tsx`
- `Navigation.tsx`
- `Form.tsx`
-

## templates

Ils défnissent la structure globale d'un page ou d'un section majeurs de l'application. On retrouve par exemple :
- DefaultPageTemplate.tsx : structure de base d'une page
- `DashboardTemplate.tsx` : Mise en page des tableaux de bord
- `ArticleTemplate.tsx` : Structure pour les pages d'articles