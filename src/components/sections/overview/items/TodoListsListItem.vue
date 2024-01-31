<template>
    <div
      class="todo-lists-list-item"
      :class="{ active: isActive, hover: isHovered }"
      @mouseenter="handleMouseEnter"
      @mouseleave="handleMouseLeave"
    >
      <h3 class="todo-list-title">{{ formatDateTitle(todoList.date) }}</h3>
      <DeleteTodoListButton 
        v-if="isHovered" 
        :activeTodoList="todoList" 
        class="delete-todo-list-button" 
        @todo-list-deleted="handleTodoListDeleted"
      />
    </div>
  </template>
  
  <script>
import DeleteTodoListButton from '@/components/base/buttons/DeleteTodoListButton.vue';

  export default {
    name: 'TodoListsListItem',
    props: {
      todoList: Object,
      isActive: Boolean
    },
    data() {
        return {
            isHovered: false,
            formattedDate: this.date
        };
    },
    methods: {
        handleMouseEnter() {
            this.isHovered = true;
        },
        handleMouseLeave() {
            this.isHovered = false;
        },
        formatDateTitle(date) {
            const options = { weekday: 'long', month: 'long', day: 'numeric' };
            const formattedDate = new Date(date).toLocaleDateString('en-US', options);
            const capitalizedMonth = formattedDate.replace(/\b\w/g, (char) => char.toUpperCase());
            return capitalizedMonth;
        },
        handleTodoListDeleted(activeTodoList) {
            this.$emit('todo-list-deleted', activeTodoList)
        }
    },
    components: { DeleteTodoListButton }
};
  </script>
  
  <style scoped>
  .todo-lists-list-item {
    cursor: pointer;
    transition: all 0.2s ease;
    display: flex;
    width: 100%;
  }

  .todo-list-title {
    text-align: left;
    padding-left: 10%;
    width: 70%;
  }
  
  .todo-lists-list-item:hover,
  .active {
    background-color: var(--primary-color);
    color: var(--default-text-color);
    transition: all 0.2s ease;
  }
  
  .hover {
    transition: all 0.2s ease;
  }

  .delete-todo-list-button {
    width: 10%;
    justify-self: flex-end;
    padding-right: 10%;
  }
  </style>