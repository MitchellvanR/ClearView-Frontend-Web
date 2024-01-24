<template>
    <div class="todo-page">
        <AppOverview class="AppOverview" :todoLists="todoLists" />
        <TodoList class="TodoList" :todoList="todoLists[0]"/>
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
                    this.formatDateTitle();
                })
                .catch(err => console.log(err.message))
        },
        sortTodoListsByDate(todoLists) {
            todoLists.sort((a, b) => {
                const dateA = Date.parse(a.date);
                const dateB = Date.parse(b.date);
                return dateA - dateB;
            })
        },
        formatDateTitle() {
            this.todoLists.forEach(todoList => {
                const options = { weekday: 'long', month: 'long', day: 'numeric' }
                const formattedDate = new Date(todoList.date).toLocaleDateString('en-US', options)

                const capitalizedMonth = formattedDate.replace(/\b\w/g, (char) => char.toUpperCase())

                todoList.title = capitalizedMonth
            });
            
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