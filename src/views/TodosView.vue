<script setup>
import { ref, watch, computed } from "vue";
import { uid } from "uid";
import { Icon } from "@iconify/vue";
import CreateTodo from "../components/CreateTodo.vue";
import TodoItem from "../components/TodoItem.vue";

// state
const todoList = ref([]);
const theme = ref("light");

// watch berfungsi untuk memberikan pengaruh (sesuai method yg digunakan) setiap kali properti yang digunakan berubah
watch(
    todoList,
    () => {
        saveToLocalStorage(); // method yang dijalankan ketika properti berubah
    },
    {
        deep: true, // allow track changes deep, jika false maka tidak akan bisa mendeteksi ketika properti di update
    }
);

const todoCompleted = computed(() => {
    // computed secara otomatis dapat mentracking dependency reactive
    // setiap array todolist update, computed akan mengevaluasi ulang
    return todoList.value.every((todo) => todo.isCompleted);
});

const fetchTodo = () => {
    const existingTodo = JSON.parse(localStorage.getItem("todolist"));
    if (existingTodo) {
        todoList.value = existingTodo;
    }
};

fetchTodo();

const saveToLocalStorage = () => {
    localStorage.setItem("todolist", JSON.stringify(todoList.value));
};

// method for save todo
const saveTodo = (todo) => {
    todoList.value.unshift({
        id: uid(),
        todo,
        isCompleted: null,
        isEditing: null,
    });
};

// method for toggle todo
const toggleTodoComplete = (todoIndex) => {
    todoList.value[todoIndex].isCompleted = !todoList.value[todoIndex].isCompleted;
};

// method for edit todo
const toggleEditTodo = (todoIndex) => {
    todoList.value[todoIndex].isEditing = !todoList.value[todoIndex].isEditing;
};

// method for update todo
const updateTodo = (todoValue, todoIndex) => {
    todoList.value[todoIndex].todo = todoValue;
};

// method for delete todo
const deleteTodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};

// method for setting theme
// const toggleTheme = () => {
//     if (theme.value == "light") {
//         theme.value = "dark";
//     } else {
//         theme.value = "light";
//     }
//     localStorage.setItem("theme", theme.value);
// };
</script>

<template>
    <main class="container">
        <h1>Create Todo 📝</h1>
        <CreateTodo @save-todo="saveTodo" />
        <ul class="todo-list">
            <TodoItem
                v-for="(todo, index) in todoList"
                :todo="todo"
                :index="index"
                @toggle-complete="toggleTodoComplete"
                @edit-todo="toggleEditTodo"
                @update-todo="updateTodo"
                @delete-todo="deleteTodo"
            />
        </ul>
        <p v-if="todoList.length < 1" class="todo-empty">
            <Icon
                icon="line-md:coffee-half-empty-twotone-loop"
                color="#42b883"
                width="24"
                height="24"
            />
            <span>Your todo is empty...</span>
        </p>
        <p v-if="todoCompleted && todoList.length > 0" class="todo-finish">
            <Icon icon="line-md:coffee-twotone-loop" color="#42b883" width="24" height="24" />
            <span>Wow, you have completed all todo!</span>
        </p>
    </main>
</template>

<style lang="scss" scoped>
main {
    // background-color: #1a1a1a;
    // color: white;
    display: flex;
    flex-direction: column;
    padding: 16px;
    min-height: 100vh;
    h1 {
        font-size: 28px;
        margin-bottom: 24px;
        text-align: center;
    }
    ul {
        margin-top: 32px;
    }
    p {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 8px;
        &.todo-empty {
            margin-top: 25%;
        }
        &.todo-finish {
            margin-top: 24px;
        }
    }
}
</style>
