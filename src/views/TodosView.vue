<script setup lang="ts">
import { ref } from 'vue';
import { uid } from 'uid';
import TodoCreator from '@/components/TodoCreator.vue';
import TodoItems from '@/components/TodoItems.vue';
import { Icon } from '@iconify/vue';

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
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItems v-for="todo in todoList" :key="todo.id" :todo="todo" />
    </ul>
    <p class="todos-msg" v-else>
      <!-- When No Todo is showing -->
      <Icon icon="noto-v1:sad-but-relieved-face" class="icon" width="22" />
      <span>You don't have anything to do!</span>
    </p>
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

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>