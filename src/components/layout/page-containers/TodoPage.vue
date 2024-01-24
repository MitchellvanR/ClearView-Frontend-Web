<template>
    <div class="todo-page">
        <AppOverview class="AppOverview" />
        <TodoList class="TodoList" />
        <TodoDetails class="TodoDetails" />
    </div>
</template>
<script>
import AppOverview from '../page-layout/AppOverview.vue'
import TodoList from '../page-layout/TodoList.vue'
import TodoDetails from '../page-layout/TodoDetails.vue'

export default {
    name: 'TodoPage',
    components: {
        AppOverview,
        TodoList,
        TodoDetails
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