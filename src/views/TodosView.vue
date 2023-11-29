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

const toggleTodoComplete = (index: number) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted
}
const toggleEditTodo = (index: number) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing
}
const updateTodo = (todo: string, index: number) => {
  todoList.value[index].todo = todo
  todoList.value[index].isEditing = false
}
const deleteTodo = (id: string) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== id)
}

</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="listenerTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItems v-for="(todo, index) in todoList" :index="index" :todo="todo" @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo" @update-todo="updateTodo" @delete-todo="deleteTodo" />
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