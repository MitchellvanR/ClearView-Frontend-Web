<template>
    <div class="delete-todo-button-wrapper">
        <div class="delete-todo-button" @click="startModal">
            <i class="fas fa-trash-alt"></i>
        </div>
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
<style scoped>
    .delete-todo-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 5rem;
        height: 5rem;
        background-color: var(--delete-button-color);
        border-radius: 50%;
        cursor: pointer;
        transition: background-color 0.3s ease-in-out;
    }

    .delete-todo-button:hover {
        background-color: var(--delete-button-hover-color);
    }

    .delete-todo-button:hover > .fa-times {
        color: var(--dark-background-text-color);
    }

    .fa-trash-alt {
        color: var(--dark-background-text-color); 
        font-size: 1.5rem; 
    }
</style>