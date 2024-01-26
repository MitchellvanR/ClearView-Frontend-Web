<template>
    <div class="todo-details">
        <TodoTitleDetails />
        <TodoDescriptionDetails />
    </div>
</template>
<script>
import TodoTitleDetails from '@/components/sections/todo-details/TodoTitleDetails.vue';
import TodoDescriptionDetails from '@/components/sections/todo-details/TodoDescriptionDetails.vue';

export default {
    name: 'TodoDetails',
    components: {
        TodoTitleDetails,
        TodoDescriptionDetails
    }
}
</script>
<style>
    .todo-details {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 7.5vh;
    }
</style>