<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="confirmation-modal-content">
            <h1>Delete Todo</h1>
            <form class="confirmation-modal-input" @submit.prevent="deleteTodo">
                <label for="deleteTodo">Are you sure you want to delete this Todo?</label>
                <input class="confirm-delete-todo-button" id="deleteTodo" type="submit" name="deleteTodo" value="Yes, delete Todo">
            </form>
        </div>
    </BaseModal>
</template>
<script>
import BaseModal from './BaseModal.vue'

export default {
    name: 'ConfirmTodoDeletionModal',
    components: {
        BaseModal
    },
    props: {
        todoList: Object,
        activeTodo: Object
    },
    methods: {
        handleModalClose() {
            this.$emit('modal-close')
        },
        async deleteTodo() {
            try {
                await fetch(`http://localhost:8080/clearview-api/todoLists/${this.todoList.title}/todos/${this.activeTodo.title}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                    }
                })
                this.$emit('todo-deleted', this.activeTodo)
                this.$emit('modal-close')
            } catch (err) {
                console.error('API request failed:', err);
            }
        }

    }
}
</script>
<style>
    .confirmation-modal-content {
        height: 80%;
        color: var(--default-text-color);
        display: flex;
        flex-direction: column;
        gap: 5rem;
    }

    .confirmation-modal-input {
        display: flex;
        flex-direction: column;
        gap: 2rem;
    }

    .confirm-delete-todo-button {
        display: block;
        align-self: center;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--delete-button-color);
        color: var(--dark-background-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .confirm-delete-todo-button:hover {
        cursor: pointer;
        background-color: var(--delete-button-hover-color);
        transition: all .2s ease;
    }
</style>