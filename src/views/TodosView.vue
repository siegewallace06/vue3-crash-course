<script setup lang="ts">
import { ref } from 'vue';
import { uid } from 'uid';
import TodoCreator from '@/components/TodoCreator.vue';

const todoList = ref<Object[]>([])
const listenerTodo = (todo: string) => {
  console.log("WOI ADA EMIT COK", todo)
  todoList.value.push({
    id: uid(),
    todo: todo,
    isCompleted: null,
    isEditing: null,

  })
  console.log("LIST BARU", todoList.value)
}

</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="listenerTodo" />
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>