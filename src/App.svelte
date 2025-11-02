<script>
  import { slide } from "svelte/transition";

  let todos = $state([]);
  let todo = $state();
  let remaining = $derived(remainingTodos());
  let filter = $state("all");
  let filteredTodos = $derived(filterTodos());

  function addTodo(e) {
    e.preventDefault();
    todos.push({ id: crypto.randomUUID(), text: todo, completed: false });
    todo = "";
  }

  function removeTodo(todo) {
    todos = todos.filter((item) => item.id !== todo.id);
  }

  function remainingTodos() {
    return todos.filter((todo) => !todo.completed).length;
  }

  function setFilter(newFilter) {
    filter = newFilter;
  }

  function clearCompleted() {
    todos = todos.filter((todo) => !todo.completed);
  }

  function filterTodos() {
    return todos.filter((todo) => {
      if (filter === "all") return true;
      if (filter === "active") return !todo.completed;
      if (filter === "completed") return todo.completed;
    });
  }
</script>

<div class="todos">
  <form onsubmit={addTodo}>
    <input type="text" placeholder="Add Todo" bind:value={todo} />
  </form>

  <ul>
    {#each filteredTodos as todo (todo)}
      <li transition:slide>
        <input type="checkbox" bind:checked={todo.completed} />
        <input type="text" bind:value={todo.text} />
        <button onclick={() => removeTodo(todo)}>X</button>
      </li>
    {/each}
  </ul>

  <div>
    <p>{remaining} {remaining === 1 ? "item" : "items"} left</p>
  </div>

  <div class="filters">
    {#each ["all", "active", "completed"] as filter}
      <button onclick={() => setFilter(filter)}>{filter}</button>
    {/each}

    <button onclick={clearCompleted}>Clear Completed</button>
  </div>
</div>
