Les requêtes GET permettent de récupérer de la données depuis le serveur.

Dans une application React, on viendras faire la requête pour récupérer les données depuis le composant qui stocke la données.

## Récupérer la donnée avec React

On ne pourras pas utiliser le `useState` pour stocker la données étant donnée que cela n'est pas pure.
A partir du moment ou l'on vient utiliser `fetch()` dans une fonction celle ci ne sera plus pure.

On viendras utiliser [[useEffect()]] pour gérer les GET.

## Utilisation

Ici, on veux récupérer une liste de todo depuis un serveur.

````javascript
function App(){

	const [todoList, setTodoList] = useState([]);
	// on ajoute un useState pour la gestion du chargement
	const [loading, setLoading] = useState(true);

	//utilisation du useEffect
	useEffect(() => {
		async function fetchTodoList(){
		//on vient placer la requête dans un bloc try 
			try{
				//on effectue la requête GET
				const response = await fetch("https://restapi.fr/api/rtodo");
				//si la réponse du serveur est ok 
				if(response.ok){
					//on vient récupérer les données depuis la réponse du serveur
					const todos = await response.json();
					//spécifique au back end de Dyma (restapi)
					if(Array.isArray(todos)){
						//on vient passer la liste de todo au setter de todoList 
						//dans le useState qui contient les todos
						setTodoList(todos);
					}else {
						setTodoList([todos]);
					}
				} else {
					console.log('Erreur');
				}
			} catch(e) {
				//dans le cas d'une erreur on affiche un message
				console.log('Erreur :' e);
			} finally {
				//on ajoute un bloc finally qui s'exécute peut importe le résultat 
				//on vient couper le loading car la requête est finex
				setLoading(false);
			}
		}
		//on appel la fonction pour déclencher l'appel
		fetchTodoList();
	}, [])
}
````

Pour la gestion du chargement, on viendras utiliser un ternaire pour afficher ou non un message.
On pourras également utiliser un gif pour une meilleur expérience utilisateur.

````javascript
return (
	//on affiche un message si la variable d'état est true
	//sinon on affiche la liste de todo
	{loading ? <p>Chargement en cours</p> : <TodoList />}
)
`````

