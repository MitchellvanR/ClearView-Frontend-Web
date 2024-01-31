<template>
    <div class="todo-lists-container">
        <TodoListsListItem 
            class="todo-lists-list-item" 
            v-for="todoList in todoLists"
            :todoList="todoList"
            :isActive="todoList.isActive"
            :key="todoList.date"
            @Click="handleItemClick(todoList.date)"
            @todo-list-deleted="handleTodoListDeleted"
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
            this.clearActiveTodos()
            this.todoLists.forEach(todoList => {
                todoList.isActive = todoList.date === clickedItem
                this.$emit('todo-list-selected')
            })
        },
        clearActiveTodos() {
            let activeTodoList = this.findActiveTodoList()
            activeTodoList.todos.forEach(todo => todo.isActive = false)
        },
        findActiveTodoList() {
            return this.todoLists.find(todoList => todoList.isActive == true);
        },
        handleTodoListDeleted(activeTodoList) {
            this.$emit('todo-list-deleted', activeTodoList)
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
        align-items: center;
    }
</style>