<template>
    <div class="todo-details">
        <TodoTitleDetails v-if="todoListsLoaded" :titleValue="findActiveTodo().title" />
        <TodoDescriptionDetails v-if="todoListsLoaded" :descriptionValue="findActiveTodo().description"/>
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
    },
    props: {
        todoListsLoaded: Boolean,
        todoList: Object
    },
    methods: {
        findActiveTodo() {
            const activeTodo = this.todoList.todos.find(todo => todo.isActive == true);
            if (activeTodo != null) return activeTodo
            return {}
        }
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