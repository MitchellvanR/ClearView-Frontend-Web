<template>
  <div 
    class="todo-list-item"
    :class="{ active: todo.isActive }"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <TodoListItemCheckbox :todo="todo" :todoList="todoList" @checkbox-toggled="updateTodoStyle" />
    <li class="todo-list-item-text" :class="{ completed: completed }">{{ todo.title }}</li>
    <DeleteTodoButton 
      class="todo-list-item-delete-button" 
      v-if="isHovered" 
      :activeTodo="activeTodo" 
      :todoList="todoList" 
      @todo-deleted="handleTodoDeletion"
    />
  </div>
</template>
<script>
import TodoListItemCheckbox from './TodoListItemCheckbox.vue';
import DeleteTodoButton from '@/components/base/buttons/DeleteTodoButton.vue';

export default {
  name: 'TodoListItem',
  components: {
    TodoListItemCheckbox,
    DeleteTodoButton
  },
  props: {
    todo: Object,
    todoList: Object,
    isActive: Boolean,
    todoListsLoaded: Boolean,
    activeTodo: Object
  },
  data() {
    return {
      completed: this.todo.completed,
      isHovered: false
    };
  },
  methods: {
    handleMouseEnter() {
      this.isHovered = true;
    },
    handleMouseLeave() {
      this.isHovered = false;
    },
    updateTodoStyle(checked, todo) {
      this.completed = checked;
      this.$emit('checkbox-toggled', checked, todo);
    },
    handleTodoDeletion(activeTodo) {
      this.$emit('todo-deleted', activeTodo);
    }
  },
};
</script>
<style scoped>
.todo-list-item {
  border-radius: 2rem 0 0 2rem;
  display: flex;
  padding: 1.5%;
  transition: all 0.2s ease;
  align-items: center;
}

.todo-list-item-text {
  list-style: none;
  margin-left: 5%;
  width: 70%;
}

.todo-list-item-delete-button {
  width: 20%;
  display: flex;
  justify-content: center;
}

.todo-list-item:hover,
.active {
  background-color: var(--tertiary-color);
  cursor: pointer;
}

.completed {
  color: var(--checked-todo-color);
  text-decoration: line-through;
}
</style>
  