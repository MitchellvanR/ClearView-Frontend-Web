<template>
    <div class="app-overview">
        <UserProfile class="user-profile" />
        <TodoLists class="todo-lists" :todoLists="todoLists" @todo-list-deleted="handleTodoListDeleted" @todo-list-selected="this.$emit('todo-list-selected')"/>
        <div class="todo-list-buttons">
            <AddTodoListButton class="add-to-list-button-wrapper" @todo-list-created="handleTodoListCreated" /> 
        </div>
    </div>
</template>
<script>
import UserProfile from '@/components/sections/overview/UserProfile.vue'
import TodoLists from '@/components/sections/overview/TodoLists.vue';
import AddTodoListButton from '@/components/base/buttons/AddTodoListButton.vue';

export default {
    name: 'AppOverview',
    components: {
    UserProfile,
    TodoLists,
    AddTodoListButton
},
    props: {
        todoLists: Array,
        activeTodoList: Object
    },
    methods: {
        handleTodoListCreated(newTodoList) {
            this.$emit('todo-list-created', newTodoList)
        },
        handleTodoListDeleted(activeTodoList) {
            this.$emit('todo-list-deleted', activeTodoList)
        }
    }
}
</script>
<style>
    .app-overview > * {
        color: var(--dark-background-text-color);
    }

    .app-overview {
        display: flex;
        flex-wrap: wrap;
    }

    .user-profile {
        width: 100%;
        height: 20%;
    }

    .todo-lists {
        width: 100%;
        height: 60%;
    }

    .todo-list-buttons {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        width: 100%;
        height: 20%;
    }
</style>