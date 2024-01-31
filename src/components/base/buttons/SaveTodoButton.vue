<template>
    <div class="add-todo-button-wrapper">
        <div class="add-todo-button" @click="updateDetails">
            <i class="fas fa-upload"></i>
        </div>
    </div>
</template>
<script>
export default {
    name: 'SaveTodoButton',
    methods: {
        updateDetails() {
            console.log('Updating details to the cloud')
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