<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="add-todo-list-modal-content">
            <h1>Add Todo List </h1>
            <form class="add-todo-list-input" @submit.prevent="createTodoList">
                <label for="date">For which date would you like to make a Todo List</label>
                <input class="add-todo-list-date-input" id="date" name="date" type="date" required>
                <input class="create-todo-list-button" type="submit" value="Create">
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
        async createTodoList() {
            try {
                const dateInput = this.$el.querySelector('.add-todo-list-date-input').value;
                let newTodoList = { title: dateInput, date: dateInput, todos: [] }
                await fetch(`http://localhost:8080/clearview-api/todoLists/`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(newTodoList)
                })
                this.$emit('todo-list-created', newTodoList)
                this.$emit('modal-close')
            } catch (err) {
                console.error('API request failed:', err);
            }
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