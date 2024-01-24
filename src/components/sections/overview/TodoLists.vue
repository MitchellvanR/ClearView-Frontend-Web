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
    data() {
        return {
            todoLists: []
        }
    },
    mounted() {
        this.fetchTodoLists()
    },
    methods: {
        fetchTodoLists() {
            fetch('http://localhost:8080/clearview-api/todoLists')
                .then(response => response.json())
                .then(data => {
                    this.todoLists = data
                    this.sortTodoListsByDate(this.todoLists);
                    if (this.todoLists.length > 0) {
                    this.todoLists[0].isActive = true
                }
                })
                .catch(err => console.log(err.message))
        },
        handleItemClick(clickedItem) {
            this.todoLists.forEach(todoList => {
                console.log(clickedItem)
                todoList.isActive = todoList.date === clickedItem
            })
        },
        sortTodoListsByDate(todoLists) {
            todoLists.sort((a, b) => {
                const dateA = Date.parse(a.date);
                const dateB = Date.parse(b.date);
                return dateA - dateB;
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