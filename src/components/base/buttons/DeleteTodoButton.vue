<template>
    <div class="delete-todo-button-wrapper">
        <button class="delete-todo-button" @click="startModal">Delete</button>
        <ConfirmTodoDeletionModal v-if="modalTrigger" :todoList="todoList" :activeTodo="activeTodo" @modal-close="modalTrigger = false" @todo-deleted="handleTodoDeletion"/>
    </div>
</template>
<script>
import ConfirmTodoDeletionModal from '../modals/ConfirmTodoDeletionModal.vue'

export default {
    name: 'DeleteTodoButton',
    components: {
        ConfirmTodoDeletionModal
    },
    props: {
        activeTodo: Object,
        todoList: Object
    },
    data() {
        return {
            modalTrigger: false
        }
    },
    methods: {
        startModal() {
            this.modalTrigger = true;
        },
        handleTodoDeletion(activeTodo) {
            this.$emit('todo-deleted', activeTodo)
        }
    }
}
</script>
<style>
    .delete-todo-button-wrapper {
        display: flex;
        justify-content: center;
    }

    .delete-todo-button {
        display: block;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--delete-button-color);
        color: var(--default-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .delete-todo-button:hover {
        cursor: pointer;
        background-color: var(--delete-button-hover-color);
        transition: all .2s ease;
    }
</style>