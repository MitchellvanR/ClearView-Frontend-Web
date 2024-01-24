<template>
    <div class="app-overview">
        <UserProfile class="user-profile" />
        <TodoLists class="todo-lists" :todoLists="todoLists" />
    </div>
</template>
<script>
import UserProfile from '@/components/sections/overview/UserProfile.vue'
import TodoLists from '@/components/sections/overview/TodoLists.vue';

export default {
    name: 'AppOverview',
    components: {
        UserProfile,
        TodoLists
    },
    props: {
        todoLists: Array
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
        height: 80%;
    }
</style>