<script>
  export let task;
  export let toggleComplete;
  export let deleteTask;
  export let openModal;
</script>

<div class="task-item">
  <div>
    <input type="checkbox" checked={task.completed} on:change={() => toggleComplete(task.id)} />
    <label>{task.title}</label>
    <div class="task-details">
      <p><strong>Date:</strong> {task.date}</p>
      <p><strong>Time:</strong> {task.time}</p>
      <p><strong>Notes:</strong> {task.note}</p>
    </div>
  </div>
  <button on:click={() => openModal(task)}>Edit</button>
  <button on:click={() => deleteTask(task.id)}>Delete</button>
  
</div>


<style>
  .task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ccc;
  }

  .task-details {
    margin-top: 5px;
    font-size: 0.9em;
    color: #555;
  }

  button {
    background-color: #ff6f00;
    color: white;
    border: none;
    cursor: pointer;
    margin-left: 10px;
  }
</style>