<script>
  import { slide } from "svelte/transition";

  let { todo, removeTodo } = $props();
</script>

<li transition:slide>
  <input type="checkbox" bind:checked={todo.completed} />
  <input type="text" bind:value={todo.text} />
  <button onclick={() => removeTodo(todo)}>X</button>
</li>
