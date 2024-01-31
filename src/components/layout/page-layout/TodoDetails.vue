<template>
    <div class="todo-details">
        <ExitButton class="exit-button-component" v-if="todoActive" :todos="todoList.todos" @todo-details-closed="this.$emit('todo-details-closed')" />
        <TodoTitleDetails class="todo-title-details" v-if="todoActive" :titleValue="findActiveTodo().title" @update-title="onUpdateTitle" />
        <TodoDescriptionDetails class="todo-description-details" v-if="todoActive" :descriptionValue="findActiveTodo().description" @update-description="onUpdateDescription"/>
        <div v-if="todoActive" class="todo-details-button-wrapper">
            <SaveTodoButton :todoList="todoList" :activeTodo="findActiveTodo()" @todo-updated="notifyTodoUpdate" />
            <DeleteTodoButtonBig :activeTodo="findActiveTodo()" :todoList="todoList" @todo-deleted="handleTodoDeleted" />
        </div>
    </div>
</template>
<script>
import ExitButton from '@/components/base/buttons/ExitButton.vue';
import TodoTitleDetails from '@/components/sections/todo-details/TodoTitleDetails.vue';
import TodoDescriptionDetails from '@/components/sections/todo-details/TodoDescriptionDetails.vue';
import SaveTodoButton from '@/components/base/buttons/SaveTodoButton.vue';
import DeleteTodoButtonBig from '@/components/base/buttons/DeleteTodoButtonBig.vue'

import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

export default {
    name: 'TodoDetails',
    components: {
    ExitButton,
    TodoTitleDetails,
    TodoDescriptionDetails,
    SaveTodoButton,
    DeleteTodoButtonBig
},
    props: {
        todoList: Object,
        todoActive: Boolean
    },
    methods: {
        findActiveTodo() {
            const activeTodo = this.todoList.todos.find(todo => todo.isActive == true);
            if (activeTodo != null) return activeTodo
            return {}
        },
        handleTodoDeleted(activeTodo) {
            this.$emit('todo-deleted', activeTodo)
        },
        onUpdateTitle(title) {
            this.findActiveTodo().title = title
        },
        onUpdateDescription(description) {
            this.findActiveTodo().description = description
        },
        notifyTodoUpdate() {
            this.$emit('todo-updated')
            toast.success('Todo successfully updated!', {
                autoClose: 3000
            })
        }
    }
}
</script>
<style>
    .todo-details {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .exit-button-component {
        height: 20%;
        width: 75%;
    }

    .todo-title-details {
        height: 20%;
    }

    .todo-description-details {
        height: 40%;
    }

    .todo-details-button-wrapper {
        display: flex;
        width: 50%;
        height: 20%;
        flex-direction: row;
        justify-content: space-evenly;
    }
</style>