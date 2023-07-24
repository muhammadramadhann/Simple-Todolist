<script setup>
import { Icon } from "@iconify/vue";

// define property (for the parent of this component)
const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },
    index: {
        type: Number,
        required: true,
    },
});

// define method (for the parent of this component)
defineEmits(["toggle-complete", "edit-todo", "update-todo", "delete-todo"]);
</script>

<template>
    <li>
        <button @click="$emit('toggle-complete', index)">
            <Icon icon="ph:check-bold" color="#42b883" width="24" />
        </button>
        <form class="todo" @submit.prevent="$emit('edit-todo', index)">
            <input
                v-if="todo.isEditing"
                :id="todo.id"
                type="text"
                :value="todo.todo"
                @input="$emit('update-todo', $event.target.value, index)"
            />
            <span :class="{ completed: todo.isCompleted }" v-else>{{ todo.todo }}</span>
        </form>
        <div class="todo-actions">
            <Icon
                v-if="!todo.isEditing"
                icon="ph:pencil"
                width="20"
                color="#35495e"
                @click="$emit('edit-todo', index)"
            />
            <Icon
                v-else
                icon="material-symbols:sync-saved-locally-outline"
                color="#35495e"
                width="20"
                height="20"
                @click="$emit('edit-todo', index)"
            />
            <Icon
                icon="ph:trash"
                width="20"
                color="#db0303"
                @click="$emit('delete-todo', todo.id)"
            />
        </div>
    </li>
</template>

<style lang="scss" scoped>
li {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    margin-bottom: 16px;
    border: 2px solid #dedede;
    border-radius: 16px;
    transition: 650ms ease;
    &:hover,
    &:active {
        .todo-actions {
            opacity: 1;
        }
    }
    button {
        border: none;
        outline: none;
        background-color: inherit;
        .iconify:hover {
            cursor: pointer;
            transform: scale(0.85);
        }
    }
    .todo {
        flex: 1;
        input {
            width: 100%;
            font-size: inherit;
            padding-bottom: 4px;
            border: none;
            border-bottom: 1px solid #dedede;
            &:active,
            &:focus {
                outline: none;
            }
        }
        .completed {
            text-decoration: line-through;
            opacity: 0.5;
        }
    }
    .todo-actions {
        opacity: 0;
        display: flex;
        gap: 8px;
        margin-left: auto;
        transition: 350ms ease-in-out;
        .iconify {
            cursor: pointer;
            &:hover {
                transform: scale(0.85);
            }
        }
    }
}
@media (max-width: 767px) {
    .todo-actions {
        opacity: 1 !important;
    }
}
</style>
