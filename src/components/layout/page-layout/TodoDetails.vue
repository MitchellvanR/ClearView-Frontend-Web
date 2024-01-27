<template>
    <div class="todo-details">
        <ExitButton v-if="todoActive" :todos="todoList.todos" @todo-details-closed="this.$emit('todo-details-closed')" />
        <TodoTitleDetails v-if="todoActive" :titleValue="findActiveTodo().title" />
        <TodoDescriptionDetails v-if="todoActive" :descriptionValue="findActiveTodo().description"/>
    </div>
</template>
<script>
import ExitButton from '@/components/base/buttons/ExitButton.vue';
import TodoTitleDetails from '@/components/sections/todo-details/TodoTitleDetails.vue';
import TodoDescriptionDetails from '@/components/sections/todo-details/TodoDescriptionDetails.vue';

export default {
    name: 'TodoDetails',
    components: {
        ExitButton,
        TodoTitleDetails,
        TodoDescriptionDetails
    },
    props: {
        todoList: Object,
        todoActive: Boolean
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