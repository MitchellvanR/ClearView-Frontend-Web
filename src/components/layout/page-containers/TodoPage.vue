<template>
    <div class="todo-page">
        <AppOverview class="AppOverview" :todoLists="todoLists" @todo-list-selected="this.todoActive = false" />
        <TodoList class="TodoList" v-if="todoListsLoaded" :todoList="findActiveTodoList()" @todo-activated="this.todoActive = true" />
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
            todoActive: false
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