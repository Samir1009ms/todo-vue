<template>
    <ul>
      <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" @remove="removeTodo" @update="updateTodo" />
    </ul>
  </template>
  
  <script>
  import TodoItem from './TodoItem.vue';
  
  export default {
    name: 'TodoList',
    components: {
      TodoItem
    },
    props: {
      todos: {
        type: Array,
        required: true
      }
    },
    methods: {
      removeTodo(id) {
        this.$emit('remove', id);
      },
      updateTodo(updatedTodo) {
        this.$emit('update', updatedTodo);
      }
    }
  };
  </script>
  