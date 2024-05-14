<template>
  <div id="app">
    <h1>To Do List</h1>
    <div class="input-container">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
      <button @click="addTask">Add Task</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" :class="{ 'completed': task.completed }">
        <div class="task-info">
          <input type="checkbox" v-model="task.completed" />
          <span>{{ task.title }}</span>
        </div>
        <div class="task-actions">
          <button class="edit-button" @click="editTask(index)">Edit</button>
          <button class="delete-button" @click="deleteTask(index)">Delete</button>
        </div>
      </li>
    </ul>
    <div v-if="editing !== null" class="edit-container">
      <input v-model="editedTask" @keyup.enter="updateTask" />
      <button @click="updateTask">Update Task</button>
      <button @click="cancelEdit">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      editing: null,
      editedTask: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ title: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    editTask(index) {
      this.editing = index;
      this.editedTask = this.tasks[index].title;
    },
    updateTask() {
      if (this.editedTask.trim() !== '') {
        this.tasks[this.editing].title = this.editedTask;
        this.cancelEdit();
      }
    },
    cancelEdit() {
      this.editing = null;
      this.editedTask = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap');

#app {
  font-family: 'Space Mono', monospace;
  text-align: center;
  margin-top: 50px;
  background-color: #e0f7fa;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

h1 {
  font-size: 2.5em;
  color: #00796b;
  margin-bottom: 20px;
}

.input-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  align-items: center;
  gap: 10px;
  background-color: #fa8072;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease;
}

input[type='text'] {
  padding: 15px;
  font-size: 18px;
  border: 2px solid #00796b;
  border-radius: 5px;
  width: 100%;
  max-width: 400px;
  transition: all 0.3s ease;
}

input[type='text']:focus {
  border-color: #ffa726;
  outline: none;
  box-shadow: 0 0 5px rgba(255, 167, 38, 0.5);
}

button {
  padding: 15px 20px;
  font-size: 18px;
  cursor: pointer;
  background-color: #ffcc80;
  color: #000;
  border: none;
  border-radius: 5px;
  font-family: 'Poppins', sans-serif;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #ffa726;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: black;
  padding: 10px;
  border: 2px solid #00796b;
  border-radius: 5px;
  margin: 10px 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s;
}

li.completed {
  background-color: #dcedc8;
}

.task-info {
  display: flex;
  align-items: center;
}

.task-info input[type='checkbox'] {
  margin-right: 10px;
}

.task-actions {
  display: flex;
  gap: 10px;
}

.edit-button {
  background-color: #4caf50;
  color: #fff;
}

.delete-button {
  background-color: #f44336;
  color: #fff;
}

.edit-button:hover {
  background-color: #388e3c;
}

.delete-button:hover {
  background-color: #d32f2f;
}

.edit-container {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 10px;
}

.edit-container input[type='text'] {
  padding: 15px;
  font-size: 18px;
  border: 2px solid #00796b;
  border-radius: 5px;
  width: 100%;
  max-width: 300px;
}
</style>
