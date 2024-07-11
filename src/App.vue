<template>
  <div id="app">
    <h1>To-Do List</h1>
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList,
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
 min-height: 400px;
  padding: 20px;
  border: 3px solid orangered;

}

h1 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 20px;
}

@media (max-width: 600px) {
  h1 {
    font-size: 1.5rem;
  }
}
</style>