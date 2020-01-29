<script>
  import { onMount } from 'svelte';
  import TodoDeleteButton from '../components/TodoDeleteButton.svelte';
  import TodoUpdateButton from '../components/TodoUpdateButton.svelte';
	import TodoInput from '../components/TodoInput.svelte';
  let todos = [];

  onMount(async () => getTodos());


  async function getTodos(){
    todos = [];
    const res = await fetch('/.netlify/functions/fauna-crud', {method: 'GET'});
    
		const json = await res.json();
		json.forEach(item => {
      const id = item.ref['@ref'].id;
			todos = [...todos, {name : item.data.name, id: id}]
    });
    console.log(todos);
  }
  
</script>

<TodoInput afterCreate={getTodos}/>

<ul>
  {#each todos as todo}
    <li>
      {todo.name}
      <TodoUpdateButton updateTodo={todo} afterUpdate={getTodos}/>
      <TodoDeleteButton id={todo.id} afterDelete={getTodos}/>
    </li>
  {/each}
</ul>

<style>
  /* your styles go here */
</style>

