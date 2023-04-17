<script>
  import Todo from './Todo.svelte';

  let todos = [];

  function addTodo() {
    todos = [...todos, { id: Date.now(), text: 'New todo', complete: false }];
  }

  function editTodo(id, text) {
    todos = todos.map(todo => {
      if (todo.id === id) {
        return { ...todo, text };
      }
      return todo;
    });
  }

  function completeTodo(id) {
    todos = todos.map(todo => {
      if (todo.id === id) {
        return { ...todo, complete: !todo.complete };
      }
      return todo;
    });
  }

  function deleteTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }
</script>

<h1>Todo List</h1>

{#if todos.length === 0}
  <p>No todos</p>
{:else}
  {#each todos as todo (todo.id)}
    <Todo
      {todo}
      on:edit={text => editTodo(todo.id, text)}
      on:complete={() => completeTodo(todo.id)}
      on:delete={() => deleteTodo(todo.id)}
    />
  {/each}
{/if}

<button on:click={addTodo}>Add todo</button>