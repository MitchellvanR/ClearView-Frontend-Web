<template>
    <div class="add-todo-button-wrapper">
        <div class="add-todo-button" @click="startModal">
            <i class="fas fa-plus"></i>
        </div>
        <AddTodoModal v-if="modalTrigger" :todoList="todoList" @modal-close="modalTrigger = false" @todo-created="handleTodoCreated"/>
    </div>
</template>
<script>
import AddTodoModal from '../modals/AddTodoModal.vue'

export default {
    name: 'AddTodoListButton',
    components: {
        AddTodoModal
    },
    props: {
        todoList: Object
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
    .add-todo-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 5rem;
        height: 5rem;
        background-color: var(--add-button-color); 
        border-radius: 50%;
        cursor: pointer;
        transition: all .2s ease;
    }

    .add-todo-button:hover {
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }

    .fa-plus {
        color: var(--dark-background-text-color); 
        font-size: 1.5rem;
    }
</style>