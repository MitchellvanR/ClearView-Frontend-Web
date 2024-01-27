<template>
    <div class="todo-lists-container">
        <TodoListsListItem 
            class="todo-lists-list-item" 
            v-for="todoList in todoLists"
            :key="todoList.date"
            :title="todoList.title"
            :date="todoList.date"
            :todos="todoList.todos"
            :isActive="todoList.isActive"
            @Click="handleItemClick(todoList.date)"
        />
    </div>
</template>
<script>
import TodoListsListItem from './items/TodoListsListItem.vue'

export default {
    name: 'TodoLists',
    components: {
        TodoListsListItem
    },
    props: {
        todoLists: Array
    },
    methods: {
        handleItemClick(clickedItem) {
            this.todoLists.forEach(todoList => {
                todoList.isActive = todoList.date === clickedItem
                this.$emit('todo-list-selected')
            })
        }
    }
}
</script>
<style>
    .todo-lists {
        display: block;
    }

    .todo-lists-list-item {
        display: flex;
        width: 100%;
        height: 8vh;
        justify-content: center;
        align-items: center;
    }
</style>