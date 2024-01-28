<template>
    <div class="add-to-list-button-wrapper">
        <button class="add-to-list-button" @click="startModal">Add</button>
        <AddTodoListModal v-if="modalTrigger" @modal-close="modalTrigger = false" @todo-list-created="handleTodoListCreated"/>
    </div>
</template>
<script>
import AddTodoListModal from '../modals/AddTodoListModal.vue'

export default {
    name: 'AddTodoListButton',
    components: {
        AddTodoListModal
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
        handleTodoListCreated(newTodoList) {
            this.$emit('todo-list-created', newTodoList)
        }
    }
}
</script>
<style>
    .add-to-list-button-wrapper {
        display: flex;
        justify-content: center;
    }

    .add-to-list-button {
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

    .add-to-list-button:hover {
        cursor: pointer;
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }
</style>