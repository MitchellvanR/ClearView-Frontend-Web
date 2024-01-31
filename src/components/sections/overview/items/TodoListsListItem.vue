<template>
    <div
      class="todo-lists-list-item"
      :class="{ active: isActive, hover: isHovered }"
      @mouseover="handleMouseOver"
      @mouseout="handleMouseOut"
      @transitionend="handleTransitionEnd"
    >
      <h3>{{ formatDateTitle(date) }}</h3>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TodoListsListItem',
    props: {
      title: String,
      date: String,
      todos: Array,
      isActive: Boolean
    },
    data() {
      return {
        isHovered: false,
        isTransitioning: false,
        formattedDate: this.date
      };
    },
    methods: {
      handleMouseOver() {
        this.isHovered = true;
        this.isTransitioning = true;
      },
      handleMouseOut() {
        this.isTransitioning = false;
      },
      handleTransitionEnd() {
        if (!this.isTransitioning) {
          this.isHovered = false;
        }
      },
      formatDateTitle(date) {
          const options = { weekday: 'long', month: 'long', day: 'numeric' }
          const formattedDate = new Date(date).toLocaleDateString('en-US', options)

          const capitalizedMonth = formattedDate.replace(/\b\w/g, (char) => char.toUpperCase())

          return capitalizedMonth
      }
    }
  };
  </script>
  
  <style scoped>
  .todo-lists-list-item {
    cursor: pointer;
    transition: background-color 0.2s ease;
  }
  
  .todo-lists-list-item:hover,
  .active {
    background-color: var(--primary-color);
    color: var(--default-text-color);
  }
  
  .hover {
    transition: background-color 0.2s ease;
  }
  </style>