<script>
  import TaskItem from './TaskItem.svelte';
  export let tasks;
  export let toggleComplete;
  export let deleteTask;
  export let openModal;
</script>

<div class="task-list">
  {#each tasks as task (task.id)}
    <TaskItem {task} {toggleComplete} {deleteTask} {openModal} />
  {/each}
</div>

<style>
  .task-list {
    margin: 20px;
  }
</style>