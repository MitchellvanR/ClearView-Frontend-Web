<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="confirmation-modal-content">
            <h1>Delete Todo List </h1>
            <form class="confirmation-modal-input" @submit.prevent="deleteTodoList">
                <label for="deleteTodoList">Are you sure you want to delete this Todo List?</label>
                <input class="confirm-delete-todo-list-button" type="submit" name="deleteTodoList" value="Yes, delete Todo List">
            </form>
        </div>
    </BaseModal>
</template>
<script>
import BaseModal from './BaseModal.vue'

export default {
    name: 'ConfirmTodoListDeletionModal',
    components: {
        BaseModal
    },
    props: {
        activeTodoList: Object
    },
    methods: {
        handleModalClose() {
            this.$emit('modal-close')
        },
        async deleteTodoList() {
            try {
                console.log(this.activeTodoList.title)
                await fetch(`http://localhost:8080/clearview-api/todoLists/${this.activeTodoList.title}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                    }
                })
                this.$emit('todo-list-deleted', this.activeTodoList)
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
        display: flex;
        flex-direction: column;
        gap: 5rem;
    }

    .confirmation-modal-input {
        display: flex;
        flex-direction: column;
        gap: 2rem;
    }

    .confirm-delete-todo-list-button {
        display: block;
        align-self: center;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--delete-button-color);
        color: var(--default-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .confirm-delete-todo-list-button:hover {
        cursor: pointer;
        background-color: var(--delete-button-hover-color);
        transition: all .2s ease;
    }
</style>