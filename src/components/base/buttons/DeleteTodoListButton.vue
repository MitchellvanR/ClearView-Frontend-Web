<template>
    <div class="delete-todo-list-button-wrapper">
        <div class="trashcan-button" @click="startModal">
            <i class="fas fa-trash-alt"></i>
        </div>
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

    .trashcan-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 3rem;
    height: 3rem;
    background-color: var(--secondary-color);
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    }

    .trashcan-button:hover {
    background-color: var(--delete-button-color);
    }

    .fa-trash-alt {
    color: var(--dark-background-text-color); 
    font-size: 1rem; 
    }
</style>