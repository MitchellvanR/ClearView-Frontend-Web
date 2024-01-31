<template>
  <label class="checkbox-container">
    <input type="checkbox" name="checkbox" class="checkbox-input" @click="updateTodoCompletionStatus"/>
    <span class="checkbox-checkmark">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="#7BC9BF" v-if="checked">
        <path d="M0 0h24v24H0V0z" fill="none"/>
        <path d="M9 16.2L4.8 12l-1.4 1.4L9 19 21 7l-1.4-1.4L9 16.2z"/>
      </svg>
    </span>
  </label>
</template>

<script>
export default {
  name: 'TodoListItemCheckbox',
  props: {
    todo: Object,
    todoList: Object
  },
  data() {
    return {
      isTogglingCheckbox: false,
      checked: this.todo.completed
    };
  },
  methods: {
    async updateTodoCompletionStatus() {
      try {
        this.toggleCheckStatus();
        await fetch(`http://localhost:8080/clearview-api/todoLists/${this.todoList.title}/todos/${this.todo.title}/`, {
          method: 'PATCH',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ completed: this.checked })
        });
      } catch (err) {
        console.error('API request failed:', err);
      }
    },
    toggleCheckStatus() {
      this.checked = !this.checked
      this.$emit('checkbox-toggled', this.checked, this.todo)
    }
  }
}
</script>
<style scoped>
.checkbox-container {
  position: relative;
  cursor: pointer;
  padding-left: 1%;
}

.checkbox-input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.checkbox-checkmark {
  height: 1.5rem;
  width: 1.5rem;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.checkbox-container:hover .checkbox-checkmark {
  background-color: var(--checkbox-hover-color);
}

.checkbox-container .checkbox-input:checked + .checkbox-checkmark {
  border: none;
}

.checkbox-checkmark svg {
  width: 100%;
  height: 100%;
}
</style>
