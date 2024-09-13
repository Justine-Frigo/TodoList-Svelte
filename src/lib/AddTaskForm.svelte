<script>
  export let addTask;
  export let editTask;
  export let existingTask;
  export let closeModal;

  let title = '';
  let date = '';
  let time = '';
  let note = '';

  
  $: title = existingTask?.title || '';
  $: date = existingTask?.date || '';
  $: time = existingTask?.time || '';
  $: note = existingTask?.note || '';

  const handleSubmit = () => {
    if (title && date && time) {
      if (existingTask) {
        editTask(existingTask.id, { title, date, time, note });
      } else {
        addTask({ title, date, time, note });
      }
      closeModal();
    }
  };
</script>

<div class="add-task-form">
  <label>
    Task Title:
    <input type="text" bind:value={title} placeholder="Task Title" />
  </label>
  
  <label>
    Date:
    <input type="date" bind:value={date} />
  </label>
  
  <label>
    Time:
    <input type="time" bind:value={time} />
  </label>
  
  <label>
    Notes:
    <textarea bind:value={note} placeholder="Add your notes here"></textarea>
  </label>
  
  <button on:click={handleSubmit}>
    {existingTask ? 'Update Task' : 'Add Task'}
  </button>
</div>

<style>
  .add-task-form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  label {
    font-weight: bold;
    margin-bottom: 5px;
  }

  input, textarea {
    padding: 8px;
    margin-bottom: 10px;
    width: 100%;
    box-sizing: border-box;
  }

  button {
    background-color: #ff6f00;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
  }
</style>
