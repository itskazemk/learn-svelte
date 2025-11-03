<script>
  import AddToTodo from "./AddToTodo.svelte";
  import TodoFilter from "./TodoFilter.svelte";
  import TodoList from "./TodoList.svelte";

  let todos = $state([]);
  let remaining = $derived(remainingTodos());
  let filter = $state("all");
  let filteredTodos = $derived(filterTodos());

  function addTodo(todo) {
    todos.push({ id: crypto.randomUUID(), text: todo, completed: false });
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
  <AddToTodo {addTodo} />

  <TodoList {filteredTodos} {removeTodo} />

  <TodoFilter   {remaining} {setFilter} {clearCompleted} />
</div>
