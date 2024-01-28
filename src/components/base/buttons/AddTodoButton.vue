<template>
    <div class="add-todo-button-wrapper">
        <button class="add-todo-button" @click="startModal">Add</button>
    </div>
    <AddTodoModal v-if="modalTrigger" @modal-close="modalTrigger = false" @todo-created="handleTodoCreated"/>
</template>
<script>
import AddTodoModal from '../modals/AddTodoModal.vue'

export default {
    name: 'AddTodoListButton',
    components: {
        AddTodoModal
    },
    data() {
        return {
            modalTrigger: false
        }
    },
    methods: {
        startModal() {
            this.modalTrigger = true
        },
        handleTodoCreated(newTodo) {
            this.$emit('todo-created', newTodo)
        }
    }
}
</script>
<style>
    .add-todo-button-wrapper {
        display: flex;
        justify-content: center;
    }

    .add-todo-button {
        display: block;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--add-button-color);
        color: var(--default-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .add-todo-button:hover {
        cursor: pointer;
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }
</style>