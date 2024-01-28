<template>
    <div class="app-overview">
        <UserProfile class="user-profile" />
        <TodoLists class="todo-lists" :todoLists="todoLists" @todo-list-selected="this.$emit('todo-list-selected')"/>
        <AddToListButton v-if="todoLists.length > 0" class="add-to-list-button-wrapper" @todo-list-created="handleTodoListCreated" /> 
    </div>
</template>
<script>
import UserProfile from '@/components/sections/overview/UserProfile.vue'
import TodoLists from '@/components/sections/overview/TodoLists.vue';
import AddToListButton from '@/components/base/buttons/AddToListButton.vue';

export default {
    name: 'AppOverview',
    components: {
        UserProfile,
        TodoLists,
        AddToListButton
    },
    props: {
        todoLists: Array
    },
    methods: {
        handleTodoListCreated(newTodoList) {
            this.$emit('todo-list-created', newTodoList)
        }
    }
}
</script>
<style>
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

    .add-to-list-button-wrapper {
        width: 100%;
        height: 20%;
    }
</style>