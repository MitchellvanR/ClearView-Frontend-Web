<template>
    <div
      class="todo-lists-list-item"
      :class="{ active: isActive, hover: isHovered }"
      @mouseover="handleMouseOver"
      @mouseout="handleMouseOut"
      @transitionend="handleTransitionEnd"
    >
      <h3>{{ title }}</h3>
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
  }
  
  .hover {
    transition: background-color 0.2s ease;
  }
  </style>