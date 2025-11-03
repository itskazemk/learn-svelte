<script>
  import { slide } from "svelte/transition";
  import TodoItem from "./TodoItem.svelte";

  let { filteredTodos, removeTodo } = $props();
</script>

<ul>
  {#each filteredTodos as todo (todo)}
    <TodoItem {todo} {removeTodo} />
  {/each}
</ul>
