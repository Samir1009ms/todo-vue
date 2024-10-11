<template>
  <li class="todo-item">
    <span :style="{ textDecoration: localTodo.completed ? 'line-through' : 'none' }">
      {{ localTodo.text }}
    </span>
    <input hidden :id="`${localTodo.id}`" type="checkbox" @click="updateTodo" v-model="localTodo.completed" />
    <label :for="`${localTodo.id}`" class="checked">
      <svg color="white" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
        class="bi bi-check-circle" viewBox="0 0 16 16">
        <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14m0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16" />
        <path
          d="m10.97 4.97-.02.022-3.473 4.425-2.093-2.094a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-1.071-1.05" />
      </svg>
    </label>
    <button @click="removeTodo">
      <svg color="white" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
        class="bi bi-trash3" viewBox="0 0 16 16">
        <path
          d="M6.5 1h3a.5.5 0 0 1 .5.5v1H6v-1a.5.5 0 0 1 .5-.5M11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3A1.5 1.5 0 0 0 5 1.5v1H1.5a.5.5 0 0 0 0 1h.538l.853 10.66A2 2 0 0 0 4.885 16h6.23a2 2 0 0 0 1.994-1.84l.853-10.66h.538a.5.5 0 0 0 0-1zm1.958 1-.846 10.58a1 1 0 0 1-.997.92h-6.23a1 1 0 0 1-.997-.92L3.042 3.5zm-7.487 1a.5.5 0 0 1 .528.47l.5 8.5a.5.5 0 0 1-.998.06L5 5.03a.5.5 0 0 1 .47-.53Zm5.058 0a.5.5 0 0 1 .47.53l-.5 8.5a.5.5 0 1 1-.998-.06l.5-8.5a.5.5 0 0 1 .528-.47M8 4.5a.5.5 0 0 1 .5.5v8.5a.5.5 0 0 1-1 0V5a.5.5 0 0 1 .5-.5" />
      </svg></button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      localTodo: { ...this.todo }
    };
  },
  methods: {
    updateTodo() {
      this.$emit('update', this.localTodo);
    },
    removeTodo() {
      this.$emit('remove', this.todo.id);
    }
  }
};
</script>

<style scoped>
.todo-item {
  margin: 10px 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  column-gap: 10px;
  list-style: none;
  background: gray;
  padding: 7px 10px;
  border-radius: 10px;
}

button {
  margin-left: 10px;
  background: transparent;
  border: none;
  cursor: pointer;
  outline: none;
}

.checked {
  cursor: pointer;
}
</style>