<template>
    <div class="todo-list-item"
      @mouseover="handleMouseOver"
      @mouseout="handleMouseOut"
    >
      <TodoListItemCheckbox :todo="todo" :todoList="todoList" @checkbox-toggled="updateTodoStyle" />
      <li class="todo-list-item-text" :class="{ completed: completed }">{{ todo.title }}</li>
    </div>
  </template>
  
  <script>
  import TodoListItemCheckbox from './TodoListItemCheckbox.vue';
  
  export default {
    name: 'TodoListItem',
    components: {
      TodoListItemCheckbox
    },
    props: {
      todo: Object,
      todoList: Object,
      isActive: Boolean
    },
    data() {
      return {
        completed: this.todo.completed
      }
    },
    methods: {
      handleMouseOver() {
        this.$emit('mouseover')
      },
      handleMouseOut() {
        this.$emit('mouseout')
      },
      updateTodoStyle(checked) {
        this.completed = checked
      }
    },
  };
  </script>
  
  <style scoped>
  .todo-list-item {
    border-radius: 2rem 0 0 2rem;
    display: flex;
    flex-direction: row;
    padding: 1rem;
    padding-left: 2rem;
    transition: all 0.2s ease;
  }
  
  .todo-list-item:hover, .active {
    background-color: var(--tertiary-color);
    cursor: pointer;
  }
  
  .completed {
    color: var(--checked-todo-color);
    text-decoration: line-through;
  }
  
  .hover {
    transition: all 0.2s ease;
  }
  
  .todo-list-item-text {
    list-style: none;
    margin-left: 5%;
  }
  </style>
  