<template>
    <div class="todo-page">
        <AppOverview class="AppOverview" :todoLists="todoLists" />
        <TodoList class="TodoList" v-if="todoLists.length > 0" :todoList="findActiveTodo"/>
        <TodoDetails class="TodoDetails" />
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
            todoLists: []
        }
    },
    computed: {
        findActiveTodo() {
            return this.todoLists.find(todoList => todoList.isActive == true);
        }
    },
    mounted() {
        this.fetchTodoLists();
    },
    methods: {
        fetchTodoLists() {
            fetch('http://localhost:8080/clearview-api/todoLists')
                .then(response => response.json())
                .then(data => {
                    this.todoLists = data
                    this.sortTodoListsByDate(this.todoLists);
                    if (this.todoLists.length > 0) this.todoLists[0].isActive = true
                })
                .catch(err => console.log(err.message))
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