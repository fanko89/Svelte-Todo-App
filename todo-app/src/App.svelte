<script>
  let todos = [
    { id: 1, title: "Todo 1", completed: false },
    { id: 2, title: "Todo 2", completed: false },
    { id: 3, title: "Todo 3", completed: true }
  ];

  let newTodo = "";
  let editingId = null;

  function addTodo() {
    const todo = {
      id: todos.length + 1,
      title: newTodo,
      completed: false
    };
    todos = [...todos, todo];
    newTodo = "";
  }

  function editTodo() {
    const index = todos.findIndex(todo => todo.id === editingId);
    todos[index].title = newTodo;
    editingId = null;
    newTodo = "";
  }

  function completeTodo(id) {
    const index = todos.findIndex(todo => todo.id === id);
    todos[index].completed = !todos[index].completed;
  }

  function deleteTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }

  function startEditing(id) {
    const index = todos.findIndex(todo => todo.id === id);
    newTodo = todos[index].title;
    editingId = id;
  }
</script>

<h1>Todo App</h1>

<ul>
  {#each todos as todo (todo.id)}
    <li>
      <label>
        <input
          type="checkbox"
          checked={todo.completed}
          on:click={() => completeTodo(todo.id)}
        />
        <span class:completed={todo.completed}>{todo.title}</span>
      </label>
      {#if editingId === todo.id}
        <div>
          <input type="text" bind:value={newTodo} />
          <button on:click={editTodo}>Save</button>
        </div>
      {:else}
        <button on:click={() => startEditing(todo.id)}>Edit</button>
        <button on:click={() => deleteTodo(todo.id)}>Delete</button>
      {/if}
    </li>
  {/each}
</ul>

<div>
  <input type="text" bind:value={newTodo} />
  <button on:click={addTodo}>Add Todo</button>
</div>

<style>
  .completed {
    text-decoration: line-through;
  }
</style>