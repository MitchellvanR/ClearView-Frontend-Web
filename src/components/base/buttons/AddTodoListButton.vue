<template>
    <div class="add-to-list-button-wrapper">
        <div class="add-to-list-button" @click="startModal">
            <i class="fas fa-plus"></i>
        </div>
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
    .add-to-list-button {
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

    .add-to-list-button:hover {
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }

    .fa-plus {
        color: var(--dark-background-text-color); 
        font-size: 1.5rem;
    }
</style>