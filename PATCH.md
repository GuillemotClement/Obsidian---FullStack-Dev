La requête PATCH permet de faire une mise à jour d'une ressource sur un serveur. La différence avec PUT c'est que ce verbe indique que l'on remplace complètement une ressource.

## Utilisation avec React

Ici, on retrouve l'application de Todo.
Dans l'application, on retrouve des boutons permettant d'éditer, de valider une todo.

Au aura au préalable préparer des fonction permettant la mise à jour des todo.

On vient ensuite créer une fonction qui permet de faire la requête pour mettre à jour une todo 

````javascript
function TodoItem({ todo, deleteTodo, updateTodo}){
	const [loading, setLoading] = useState(false);
	
	async function tryUpdateTodo(newTodo){
		try{
			setLoading(true);
			//on viens déconstruire la todo au préalable pour retirer l'id
			const { _id, ...newTodoWithoutId } = newTodo;
			//on configure la requête
			const response = await fetch(`https://restapi.fr/api/rtodo/api/${todo._id}`, {
				method: 'PATCH',
				//on lui passe la nouvelle todo que l'on passe en param
				//il ne faut pas passer l'id pour eviter une erreur
				body: JSON.stringify(newTodoWithoutId),
				headers: {
					'Content-Type': 'application/json'
				}
			});
			//on vérifie ensuite que la réponse est ok
			if(response.ok){
				const newTodo = await response.json();
				updateTodo(newTodo);
			} else {
				console.log('Erreur');
			}
		} catch(e){
			console.log(e);
		} finally {
			setLoading(false);
		}
	}
}

````




