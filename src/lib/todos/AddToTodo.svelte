<script>
  let { addTodo } = $props();

  let todo = $state();

  function onsubmit(e) {
    e.preventDefault();
    addTodo(todo);
    todo = "";
  }
</script>

<form {onsubmit}>
  <input type="text" placeholder="Add Todo" bind:value={todo} />
</form>
