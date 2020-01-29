<script>
  export let id = null;
  export let afterDelete = () => {};

  async function deletetodo(){
    const res = await fetch(`/.netlify/functions/fauna-crud/${id}`, {method:'DELETE'});
    const data = await res.json();
    afterDelete();
  }
</script>

<button on:click={deletetodo}>Delete</button>

<style>
  /* your styles go here */
</style>

