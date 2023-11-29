<script setup>
import { ref, reactive } from 'vue';

import TodoButton from '@/components/TodoButton.vue';
// const todo = ref("")
const todoState = reactive({
    todo: "",
    invalid: null,
    error: "",
})

const emit = defineEmits(['create-todo'])


const createTodo = () => {
    if (todoState.todo !== "") {
        emit('create-todo', todoState.todo)
        todoState.todo = ""
        todoState.invalid = null
        return;
    }
    todoState.invalid = true
    todoState.error = "Todo cannot be empty"

}

</script>
console.log(todoState)
<template>
    <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
        <input type="text" v-model="todoState.todo" />
        <!-- <button @click="createTodo()">Create</button> -->
        <TodoButton @click="createTodo()"> Create! </TodoButton>

    </div>
    <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.error }}</p> -->
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.error }}</p>
</template>


<style lang="scss" scoped>
.input-wrap {
    display: flex;
    transition: 250ms ease;
    border: 2px solid #41b080;

    &.input-err {
        border-color: red;
    }

    &:focus-within {
        box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
    }

    input {
        width: 100%;
        padding: 8px 6px;
        border: none;

        &:focus {
            outline: none;
        }
    }

    button {
        padding: 8px 16px;
        border: none;
    }
}

.err-msg {
    margin-top: 6px;
    font-size: 12px;
    text-align: center;
    color: red;
}
</style>