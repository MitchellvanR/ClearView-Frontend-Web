<template>
    <div class="delete-todo-list-button-wrapper">
        <button class="delete-todo-list-button" @click="startModal">Delete</button>
        <ConfirmTodoListDeletionModal v-if="modalTrigger" :activeTodoList="activeTodoList" @modal-close="modalTrigger = false" @todo-list-deleted="handleTodoListDeletion"/>
    </div>
</template>
<script>
import ConfirmTodoListDeletionModal from '../modals/ConfirmTodoListDeletionModal.vue'

export default {
    name: 'DeleteTodoListButton',
    components: {
        ConfirmTodoListDeletionModal
    },
    props: {
        activeTodoList: Object
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
        handleTodoListDeletion(activeTodoList) {
            this.$emit('todo-list-deleted', activeTodoList)
        }
    }
}
</script>
<style>
    .delete-todo-list-button-wrapper {
        display: flex;
        justify-content: center;
    }

    .delete-todo-list-button {
        display: block;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--delete-button-color);
        color: var(--dark-background-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .delete-todo-list-button:hover {
        cursor: pointer;
        background-color: var(--delete-button-hover-color);
        transition: all .2s ease;
    }
</style>