<template>
    <div class="add-todo-button-wrapper">
        <div class="add-todo-button" @click="updateTodoDetails">
            <i class="fas fa-upload"></i>
        </div>
    </div>
</template>
<script>
export default {
    name: 'SaveTodoButton',
    props: {
        activeTodo: Object,
        toChangeTodo: Object,
        todoList: Object
    },
    methods: {
        async updateTodoDetails() {
            if (this.toChangeTodo.title == "") {
                this.$emit('invalid-input')
                return
            }
            try {
                await fetch(`http://localhost:8080/clearview-api/todoLists/${this.todoList.title}/todos/${this.activeTodo.title}/`, {
                method: 'PATCH',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(this.toChangeTodo)
                });
                this.updateActiveTodo()
            } catch (err) {
                console.error('API request failed:', err);
            }
        },
        updateActiveTodo() {
            let newTodo = this.toChangeTodo
            if (!newTodo.title) newTodo.title = this.activeTodo.title
            if (!newTodo.description) newTodo.description = this.activeTodo.description
            newTodo.completed = this.activeTodo.completed
            this.$emit('todo-updated', newTodo)
        }
    }
}
</script>
<style>
.add-todo-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 5rem;
    height: 5rem;
    background-color: var(--add-button-color); 
    border-radius: 50%;
    cursor: pointer;
    transition: all .2s ease;
}

.add-todo-button:hover {
    background-color: var(--add-button-hover-color);
    transition: all .2s ease;
}

.fa-upload {
    color: var(--dark-background-text-color); 
    font-size: 1.5rem;
}
</style>