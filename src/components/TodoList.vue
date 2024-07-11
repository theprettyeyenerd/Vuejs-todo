<template>
  <div class="todo-list">
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <span :class="{ completed: task.completed }" @click="toggleTask(index)">
          {{ task.text }}
        </span>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
    <div class="filters">
      <button @click="filter = 'all'">All</button>
      <button @click="filter = 'completed'">Completed</button>
      <button @click="filter = 'incomplete'">Incomplete</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: JSON.parse(localStorage.getItem('tasks') || '[]'),
      filter: 'all',
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter((task) => task.completed);
      } else if (this.filter === 'incomplete') {
        return this.tasks.filter((task) => !task.completed);
      } else {
        return this.tasks;
      }
    },
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
        this.saveTasks();
      }
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
      this.saveTasks();
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
  },
};
</script>

<style scoped>
.todo-list {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 10px;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  box-sizing: border-box;
  font-size: 1rem;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  cursor: pointer;
}

button {
  background-color: #ff0000;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

button:hover {
  background-color: #cc0000;
}

.filters {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.filters button {
  flex: 1;
  margin: 0 5px;
}

@media (max-width: 600px) {
  .todo-list {
    padding: 10px;
  }

  input {
    font-size: 0.875rem;
  }

  li {
    padding: 8px;
  }

  button {
    padding: 5px;
  }
}
</style>
