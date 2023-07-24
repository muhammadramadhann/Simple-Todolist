<script setup>
import { reactive, ref } from "vue";
import { Icon } from "@iconify/vue";

const emit = defineEmits(["save-todo"]);

const todoState = reactive({
    todo: "",
    invalid: null,
    errorMsg: "",
});

const info = ref(false);

const saveTodo = () => {
    todoState.invalid = null;
    if (todoState.todo.trim() === "") {
        todoState.invalid = true;
        todoState.errorMsg = "Todo value cannot be empty!";
        return;
    }

    emit("save-todo", todoState.todo);
    todoState.todo = "";
};

const toggleInfo = () => {
    info.value = !info.value;
};

const toggleBlueInfo = () => {
    info.value = false;
};
</script>

<template>
    <form @submit.prevent="saveTodo" class="input-wrap">
        <input id="todo" type="text" v-model="todoState.todo" placeholder="➡️ Enter to save" />
        <div class="todo-button">
            <span class="info" :class="{ show: info }">Under development</span>
            <button type="button" @click="toggleInfo" @blur="toggleBlueInfo">
                <Icon
                    icon="line-md:moon-to-sunny-outline-loop-transition"
                    color="#42b883"
                    width="18"
                />
            </button>
            <button type="submit">Save Todo</button>
        </div>
    </form>
    <p v-show="todoState.invalid" class="error-msg">{{ todoState.errorMsg }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
    display: flex;
    transition: 250ms ease;
    input {
        font-size: 17px;
        width: 100%;
        padding: 8px;
        border: none;
        border-bottom: 1px solid #dedede;
        &:active,
        &:focus {
            box-shadow: 0px 2px 1px 0px rgba(0, 0, 0, 0.08);
            outline: none;
        }
    }
    .todo-button {
        visibility: hidden;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 16px;
        position: fixed;
        bottom: 0;
        left: 0;
        padding: 16px;
        border-top: 1px solid #dedede;
        background-color: #ffffff;
        button {
            cursor: pointer;
            font-size: 17px;
            font-weight: bold;
            border: none;
            outline: none;
            border-radius: 16px;
        }
        button[type="submit"] {
            width: 100%;
            padding: 12px 18px;
            color: white;
            background-color: #42b883;
        }
        button[type="button"] {
            color: #42b883;
            padding: 9px 18px 12px 18px;
            border: 1px solid #42b883;
            background-color: transparent;
            .iconify {
                vertical-align: middle;
            }
        }
        .info {
            transition: 200ms ease-in-out;
            z-index: -100;
            position: absolute;
            font-size: 14px;
            padding: 12px 18px;
            border-radius: 12px;
            background-color: #dedede;
            left: -200px;
            bottom: 88px;
            &.show {
                left: 16px;
            }
        }
    }
}
@media (max-width: 767px) {
    .todo-button {
        visibility: visible !important;
    }
}
.error-msg {
    margin-top: 8px;
    font-size: 14px;
    color: #db0303;
}
</style>
