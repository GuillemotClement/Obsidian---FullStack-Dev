Ce hook natif permet aux composants de se synchroniser avec des système externes en permettant d'exécuter du code après le rendu du composant.

## Utilisation 
- Contrôle d'un composant non géré par React (provenant d'une librairie tierce par exemple)
- Effectuer une connexion à un serveur (une connexion `Websocker` à un chat par exemple)
- Effectuer des requête HTTP de type `ajax` avec `fetch()` pour récupérer de la données.

## Déclaration 
La syntaxe d'un `useEffect()`: 

```javascript
//importation du hook depuis react
import { useEffect } from 'react';

export default function MonComposant(){
	useEffect(() => {
		//code exécuté après chaque rendu
	});
	return (
		//rendu du composant
	)
}
```

Par défaut, un effet est exécuté après chaque rendu.

