<script>
  export let updateTodo;
  let isUpdating = false;
  export let afterUpdate = () => {};

  async function updateTodoItem(){
    const res = await fetch(
      `/.netlify/functions/fauna-crud/${updateTodo.id}`, 
      {
        method:'PUT',
        body: JSON.stringify(updateTodo)
      }
    );
    isUpdating = false;
    
    afterUpdate();
  }

</script>



{#if isUpdating}
  <input type="text" bind:value={updateTodo.name}>
  <button on:click={updateTodoItem}>Submit</button>
{:else}
  <button on:click={() => {isUpdating = true}}>Update</button>
{/if}

<style>
  /* your styles go here */
</style>

