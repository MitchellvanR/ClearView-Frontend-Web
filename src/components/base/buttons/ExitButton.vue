<template>
    <div class="exit-button-wrapper">
        <button class="exit-button" @click="clearActiveTodos">X</button>
    </div>
</template>
<script>
export default {
    name: 'ExitButton',
    props: {
        todos: Array
    },
    methods: {
        clearActiveTodos() {
            this.todos.forEach(todo => todo.isActive = false);
            this.$emit('todo-details-closed')
        }
    }
}
</script>
<style>
    .exit-button-wrapper {
        display: flex;
        flex-wrap: wrap;
        width: 80%;
        justify-content: right;
    }

    .exit-button {
        background-color: var(--exit-button-background-color);
        border-radius: 50%;
        border: none;
        font-size: 1.5vw;
        color: var(--exit-button-text-color);
        margin-top: 2vh;
        width: 2.5vw;
        height: 2.5vw;
        transition: all .3s ease;
    }

    .exit-button:hover {
        cursor: pointer;
        background-color: var(--exit-button-text-color);
        color: var(--exit-button-background-color);
        transition: all .3s ease;
    }
</style>