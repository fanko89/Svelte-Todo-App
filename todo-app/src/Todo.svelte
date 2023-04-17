<script>
    export let todo;
    export let onEdit;
    export let onDelete;
    export let onComplete;
    let isEditing = false;
    let editText = todo.text;
  
    function handleEditClick() {
      isEditing = true;
    }
  
    function handleSaveClick() {
      todo.text = editText;
      onEdit(todo);
      isEditing = false;
    }
  
    function handleCancelClick() {
      isEditing = false;
    }
  
    function handleDeleteClick() {
      onDelete(todo);
    }
  
    function handleCompleteClick() {
      onComplete(todo);
    }
  </script>
  
  <div class="{todo.completed ? 'completed' : ''}">
    {#if isEditing}
      <input type="text" bind:value={editText}>
      <button on:click={handleSaveClick}>Save</button>
      <button on:click={handleCancelClick}>Cancel</button>
    {:else}
      <span>{todo.text}</span>
      <button on:click={handleEditClick}>Edit</button>
      <button on:click={handleDeleteClick}>Delete</button>
      {#if !todo.completed}
        <button on:click={handleCompleteClick}>Complete</button>
      {/if}
    {/if}
  </div>
  
  <style>
    .completed {
      text-decoration: line-through;
    }
  </style>

  
  
  