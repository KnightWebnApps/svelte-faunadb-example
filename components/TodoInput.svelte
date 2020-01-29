<script>
export let afterCreate = () => {};
  let todo = {
    name : ''
  }

  async function createTodo() {
		const res = await fetch('/.netlify/functions/fauna-crud', {
			body: JSON.stringify(todo),
			method: 'POST'
    });
    const data = res.json();
    console.log(res.statusText);
    todo.name = '';
    afterCreate();
	}
</script>
  <label for="todo-input">
    <input bind:value={todo.name} type="text" name="todo-input">
    <button type="submit" on:click={createTodo}>Add Todo Sucka</button>
  </label>


<style>
  /* your styles go here */
</style>

