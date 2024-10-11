<template>
  <div id="app">
    <h1>My Todo List</h1>
      <div class="add-todo">
        <input class="add-todo-input" v-model="newTodoText" @keyup.enter="addTodo" placeholder="Add a new todo" />
        <button class="add-todo-button" @click="addTodo">Add</button>
      </div>
    <TodoList :todos="todos" @remove="removeTodo" @update="updateTodo" />
  </div>
</template>

<script>
import axios from 'axios';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList
  },
  data() {
    return {
      todos: [],
      newTodoText: ''
    };
  },
  created() {
    this.fetchTodos();
  },
  methods: {
    async fetchTodos() {
      const response = await axios.get('http://localhost:3000/todos');
      this.todos = response.data;
    },
    async addTodo() {
      if (this.newTodoText.trim() === '') return;

      const newTodo = {
        text: this.newTodoText,
        completed: false
      };

      const response = await axios.post('http://localhost:3000/todos', newTodo);
      this.todos.push(response.data);
      this.newTodoText = '';
    },
    async removeTodo(id) {
      await axios.delete(`http://localhost:3000/todos/${id}`);
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    async updateTodo(updatedTodo) {
      await axios.put(`http://localhost:3000/todos/${updatedTodo.id}`, updatedTodo);
      const index = this.todos.findIndex(todo => todo.id === updatedTodo.id);
      this.todos.splice(index, 1, updatedTodo);
    }
  }
};
</script>

<style>
  #app{
    width: 100%;
    height: 100vh;
    background-color: rgba(35, 47, 72, 0.892);
    display: flex;
    align-items: center;
    justify-content: start;
    flex-direction: column;
    row-gap: 10px ;
  }

  .add-todo{
      width: 300px;
  }

  .add-todo-input{
    width: 80%;
    height: 30px;
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
    border: none;
    outline: none;
    text-indent: 10px;
    background-color: rgb(24, 24, 24);
    color: #fff;
  }
  .add-todo-button{
    width: 20%;
    height: 30px;
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    border: none;
    outline: none;
    background-color: #fff;
    cursor: pointer;

  }

  h1{
    color: #fff;
  }


</style>