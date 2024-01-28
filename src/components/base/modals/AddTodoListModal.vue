<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="add-todo-list-modal-content">
            <h1>Add Todo List </h1>
            <form class="add-todo-list-input" @submit.prevent="createTodoList">
                <label for="date">For which date would you like to make a Todo List</label>
                <input class="add-todo-list-date-input" name="date" type="date" required>
                <button class="create-todo-list-button" type="submit">Create</button>
            </form>
        </div>
    </BaseModal>
</template>
<script>
import BaseModal from './BaseModal.vue'

export default {
    name: 'AddTodoListModal',
    components: {
        BaseModal
    },
    methods: {
        handleModalClose() {
            this.$emit('modal-close')
        },
        createTodoList() {
            console.log('Creating todo list...')
            
            this.$emit('modal-close')
        }
    }
}
</script>
<style>
    .add-todo-list-modal-content {
        height: 80%;
        display: flex;
        flex-direction: column;
        gap: 5rem;
    }

    .add-todo-list-input {
        display: flex;
        flex-direction: column;
        gap: 2rem;
    }

    .add-todo-list-date-input {
        font-size: 100%;
        background-color: var(--input-offwhite-color);
        box-sizing: border-box;
        padding: 0 1rem;
        border: none;
        border-radius: .5rem;
        height: 5vh;
        width: 100%;
    }

    .create-todo-list-button {
        display: block;
        align-self: center;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--add-button-color);
        color: var(--default-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .create-todo-list-button:hover {
        cursor: pointer;
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }
</style>