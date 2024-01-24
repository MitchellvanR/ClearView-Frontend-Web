<template>
    <label class="checkbox-container">
      <input type="checkbox" v-model="isChecked" class="checkbox-input" @click.stop="toggleCheckbox" />
      <span class="checkbox-checkmark">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="#7BC9BF" v-if="isChecked">
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
        isChecked: this.todo.completed || false
      };
    },
    methods: {
      toggleCheckbox() {
        this.isChecked = !this.isChecked;
        this.$emit('checkbox-toggled', this.isChecked);
        this.updateTodoCompletionStatus();
      },
      updateTodoCompletionStatus() {
        fetch('http://localhost:8080/clearview-api/todoLists/' + this.todoList.title + '/todos/' + this.todo.title + '/', {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ completed: this.isChecked })
        })
        .catch(err => console.error('Error patching data:', err));
      }
    }
  }
  </script>
  
  <style>
  .checkbox-container {
    display: inline-block;
    position: relative;
    padding-left: 25px;
    cursor: pointer;
  }
  
  .checkbox-input {
    position: absolute;
    opacity: 0;
    cursor: pointer;
  }
  
  .checkbox-checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 25px;
    width: 25px;
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
  