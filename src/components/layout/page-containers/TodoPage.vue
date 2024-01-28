<template>
    <div class="todo-page">
        <AppOverview 
            class="AppOverview" 
            :todoLists="todoLists" 
            :activeTodoList="findActiveTodoList()" 
            @todo-list-selected="this.todoActive = false" 
            @todo-list-created="handleTodoListCreated"
            @todo-list-deleted="handleTodoListDeleted"
        />
        <TodoList 
            class="TodoList" 
            :todoList="findActiveTodoList()" 
            :todoListsLoaded="todoListsLoaded"
            @todo-activated="this.todoActive = true" 
            @todo-created="handleTodoCreated"
            @todo-deleted="handleTodoDeleted"
        />
        <TodoDetails class="TodoDetails" :todoList="findActiveTodoList()" :todoActive="todoActive" @todo-details-closed="this.todoActive = false" />
    </div>
</template>
<script>
import AppOverview from '@/components/layout/page-layout/AppOverview.vue'
import TodoList from '../page-layout/TodoList.vue'
import TodoDetails from '../page-layout/TodoDetails.vue'

export default {
    name: 'TodoPage',
    components: {
        AppOverview,
        TodoList,
        TodoDetails
    },
    data() {
        return {
            todoLists: [],
            todoActive: false,
            todoListsLoaded: false
        }
    },
    mounted() {
        this.fetchTodoLists();
    },
    methods: {
        async fetchTodoLists() {
            try {
                const response = await fetch('http://localhost:8080/clearview-api/todoLists');
                const data = await response.json();
                this.todoLists = data;
                this.sortTodoListsByDate(this.todoLists);
                if (this.todoLists.length > 0) {
                    this.todoLists[0].isActive = true
                    this.todoListsLoaded = true;
                }
            } catch (error) {
                console.log(error.message);
            }
        },
        sortTodoListsByDate(todoLists) {
            todoLists.sort((a, b) => {
                const dateA = Date.parse(a.date);
                const dateB = Date.parse(b.date);
                return dateA - dateB;
            })
        },
        findActiveTodoList() {
            return this.todoLists.find(todoList => todoList.isActive == true);
        },
        handleTodoListCreated(newTodoList) {
            this.todoLists.push(newTodoList)
            this.clearActiveTodos()
            this.clearActiveTodoLists()
            this.sortTodoListsByDate(this.todoLists)
            this.todoListsLoaded = true
            newTodoList.isActive = true
        },
        handleTodoListDeleted(activeTodoList) {
            this.todoLists.splice(this.todoLists.indexOf(activeTodoList), 1)
            this.sortTodoListsByDate(this.todoLists)
            if (this.todoLists.length <= 0) {
                this.todoListsLoaded = false
                return
            }
            this.todoLists[0].isActive = true;
        },
        clearActiveTodoLists() {
            this.todoLists.forEach(todoList => todoList.isActive = false)
        },
        clearActiveTodos() {
            this.findActiveTodoList().todos.forEach(todo => todo.isActive = false)
            this.todoActive = false
        },
        handleTodoCreated(newTodo) {
            this.findActiveTodoList().todos.push(newTodo)
            this.clearActiveTodos()
            newTodo.isActive = true;
            this.todoActive = true;

        },
        handleTodoDeleted(activeTodo) {
            this.findActiveTodoList().todos.splice(this.findActiveTodoList().todos.indexOf(activeTodo), 1)
            this.clearActiveTodos()
        }
    }
}
</script>
<style>
.todo-page {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.AppOverview {
    background-color: var(--secondary-color);
    flex: 1;
    width: 25vw;
    height: 100vh;
}

.TodoList {
    background-color: var(--primary-color);
    flex: 2;
    width: 50vw;
    height: 100vh;
}

.TodoDetails {
    background-color: var(--tertiary-color);
    flex: 1;
    width: 25vw;
    height: 100vh;
}

/* Adjust the styles for mobile devices */
@media (max-width: 768px) {
  .AppOverview, .TodoList, .TodoDetails {
    width: 100%;
    flex: 1 0 100%;
  }
}
</style>