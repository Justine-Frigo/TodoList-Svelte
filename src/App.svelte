<script>
  import Header from './lib/Header.svelte';
  import TaskList from './lib/TaskList.svelte';
  import AddTaskForm from './lib/AddTaskForm.svelte';
  import Modal from './lib/Modal.svelte';

  let tasks = [];
  let showModal = false;
  let taskToEdit = null;

  const loadTasks = () => {
    const savedTasks = JSON.parse(localStorage.getItem('tasks')) || [];
    tasks = savedTasks;
  };

  const saveTasks = () => {
    localStorage.setItem('tasks', JSON.stringify(tasks));
  };

  const addTask = (newTask) => {
    tasks = [...tasks, { id: Date.now(), ...newTask, completed: false }];
    saveTasks();
  };

  const editTask = (id, updatedTask) => {
    tasks = tasks.map(task => task.id === id ? { ...task, ...updatedTask } : task);
    saveTasks();
  };

  const deleteTask = (id) => {
    tasks = tasks.filter(task => task.id !== id);
    saveTasks();
  };

  const toggleComplete = (id) => {
    tasks = tasks.map(task => task.id === id ? { ...task, completed: !task.completed } : task);
    saveTasks();
  };

  const openModal = (task = null) => {
    taskToEdit = task;
    showModal = true;
  };

  const closeModal = () => {
    showModal = false;
    taskToEdit = null;
  };

  loadTasks();
</script>

<Header />
<button on:click={() => openModal()}>Add New Task</button>
<TaskList {tasks} {toggleComplete} {deleteTask} {openModal} />
<Modal {showModal} {closeModal}>
  <AddTaskForm {addTask} {editTask} existingTask={taskToEdit} {closeModal} />
</Modal>

<style>
  
  button {
    background-color: #ff6f00;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    margin-bottom: 20px;
  }
</style>