<template>
    <div class="todo-list-content-wrapper">
        <div class="todo-list">
            <div class="buffer"></div>
            <div class="todo-list-wrapper">
                <h1 class="todo-list-title">{{ formatDateTitle(todoList) }}</h1>
                <ul class="todo-list-unordered-list">
                    <TodoListItem 
                        class="todo-list-item"
                        v-for="todo in todoList.todos" 
                        :key="todo.title"
                        :todo="todo"
                        :todoList="todoList"
                        :isActive="todo.isActive"
                        @checkbox-toggled="updateTodo"
                        @click="handleListItemClick(todo.title)"
                    />
                </ul>
            </div>
        </div>
        <div class="todo-list-buttons">
            <AddTodoButton :todoList="todoList" @todo-created="handleTodoCreated" />
        </div>
    </div>
  </template>
  
  <script>
  import AddTodoButton from '@/components/base/buttons/AddTodoButton.vue';
import TodoListItem from '../../sections/todo-list/TodoListItem.vue';
  
  export default {
    name: 'TodoList',
    components: {
    TodoListItem,
    AddTodoButton
},
    props: {
      todoList: Object
    },
    methods: {
        handleListItemClick(title) {
            this.todoList.todos.forEach(todo => {
                todo.isActive = todo.title === title
            })
            this.$emit('todo-activated')
        },
        formatDateTitle(todoList) {
            const options = { weekday: 'long', month: 'long', day: 'numeric' }
            const formattedDate = new Date(todoList.date).toLocaleDateString('en-US', options)
            const capitalizedMonth = formattedDate.replace(/\b\w/g, (char) => char.toUpperCase())
            return capitalizedMonth
        },
        updateTodo(checked, todo) {
            const originalTodo = this.todoList.todos.find(element => element === todo)
            originalTodo.completed = checked
        },
        handleTodoCreated(newTodo) {
            this.$emit('todo-created', newTodo)
        }
    }
}
</script>
<style>
    .todo-list-content-wrapper {
        display: flex;
        flex-direction: column;
    }

    .todo-list {
        display: grid;
        grid-template-columns: 1fr 2.5fr;
        grid-template-rows: 1fr;
        height: 80%;
    }

    .todo-list-wrapper {
        display: flex;
        flex-direction: column;
        text-align: left;
        margin-top: 35%;
        overflow: scroll;
        padding-bottom: 1rem;
    }

    .todo-list-unordered-list {
        overflow: scroll;
    }

    .todo-list-title {
        margin-bottom: 3%;
    }

    .todo-list-buttons {
        height: 20%;
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        align-items: flex-start;
    }

    /* Adjust the styles for mobile devices */
    @media (max-width: 1200px) {
        .todo-list {
            grid-template-columns: .5fr 3fr;

        }
    }

    @media (max-width: 768px) {
        .buffer {
            display: none;
        }

        .todo-list-content-wrapper {
            width: 100%;
        }

        .todo-list-item {
            border-radius: none;
        }

        .todo-list {
            grid-template-columns: .5fr 3fr;

        }
    }
</style>