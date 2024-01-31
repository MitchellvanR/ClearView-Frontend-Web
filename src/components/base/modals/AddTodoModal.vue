<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="add-todo-modal-content">
            <h1>Add Todo</h1>
            <form class="add-todo-input" @submit.prevent="createTodo">
                <label ref="titleInput" for="title">What would you like to do:</label>
                <input class="add-todo-title-input" id="title" name="title" type="text" required>
                <label for="description">Add a description:</label>
                <textarea class="add-todo-description-input" id="description" name="description" type="text" rows="7"></textarea>
                <input class="create-todo-button" type="submit" value="Create">
            </form>
        </div>
    </BaseModal>
</template>
<script>
import BaseModal from './BaseModal.vue'
export default {
    name: 'AddTodoModal',
    components: {
        BaseModal
    },
    props: {
        todoList: Object
    },
    data() {
        return {
            isModalOpen: false
        }
    },
    watch: {
        isModalOpen(newValue) {
            if (newValue) {
                this.$nextTick(() => {
                    this.$refs.titleInput.focus()
                })
            }
        }
    },
    mounted() {
        this.isModalOpen = true;
    },
    methods: {
        async createTodo() {
            const todoTitle = this.$el.querySelector('.add-todo-title-input').value;
            const todoDescription = this.$el.querySelector('.add-todo-description-input').value != null ? this.$el.querySelector('.add-todo-description-input').value : "";
            const newTodo = { title: todoTitle, description: todoDescription, completed: false }

            await fetch(`http://localhost:8080/clearview-api/todoLists/${this.todoList.title}/todos/`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(newTodo)
            })
                
            this.$emit('todo-created', newTodo)
            this.$emit('modal-close')
            this.isModalOpen = false;
        },
        handleModalClose() {
            this.$emit('modal-close')
            this.isModalOpen = false;
        }
    }
}
</script>
<style>
    .add-todo-modal-content {
        height: 80%;
        display: flex;
        flex-direction: column;
        gap: 2rem;
        width: 50%;
    }

    .add-todo-input {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .add-todo-title-input {
        font-size: 100%;
        background-color: var(--input-offwhite-color);
        box-sizing: border-box;
        padding: 0 1rem;
        border: none;
        border-radius: .5rem;
        height: 5vh;
        width: 100%;
    }

    .add-todo-description-input {
        font-size: 100%;
        background-color: var(--input-offwhite-color);
        box-sizing: border-box;
        padding: 0 1rem;
        border: none;
        border-radius: .5rem;
        width: 100%;
        resize: none;
    }

    .create-todo-button {
        margin-top: 1rem;
        display: block;
        align-self: center;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--add-button-color);
        color: var(--dark-background-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .create-todo-button:hover {
        cursor: pointer;
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }
</style>