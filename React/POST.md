```javascript 
async function createTodo() {
//on utilise un bloc try si echec
	try {
	  setLoading(true);
	  setError(null);
	  //on réalise la requête avec await
	  //vers url du serveur
	  //le tableau d'option
	  const reponse = await fetch('https://restapi.fr/api/todo', {
		method: 'POST',
		headers: {
		  'Content-Type': 'application/json',
		},
		//ici la todo convertis en json
		body: JSON.stringify({
		  content: value,
		  edit: false,
		  done: false,
		}),
	  });
	  //on vérifie que la requête s'est bien déroulé
		if (reponse.ok) {
		//la todo est créer et on la récupère
			const todo = await reponse.json();
			//in passe la nouvelle todo à la fonction addTodoL
			addTodo(todo);
			setValue('');
		} else {
			setError('Oops, une erreur');
		}
	} catch (e) {
	  setError('Oops, une erreur');
	} finally {
	  setLoading(false);
	}
}
```

Les requête POST sont des requêtes qui permettent d'ajouter de la données sur un serveur, dans une base de données.
