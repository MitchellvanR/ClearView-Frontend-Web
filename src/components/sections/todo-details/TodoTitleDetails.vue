<template>
    <div class="todo-title-details">
        <h2><label for="title-box">Title: </label></h2>
        <input id="title-box" name="title-box" type="text" :value="titleValue" @input="updateTitle">
    </div>
</template>
<script>
export default {
    name: 'TodoTitleDetails',
    props: {
        titleValue: String
    },
    methods: {
        updateTitle(event) {
            this.$emit('update-title', event.target.value);
        }
    }
}
</script>
<style>
    .todo-title-details {
        display: flex;
        flex-direction: column;
        text-align: left;
        gap: 1rem;
        margin-top: 5vh;
        width: 75%;
    }

    #title-box {
        font-size: 100%;
        box-sizing: border-box;
        padding: 0 1rem;
        border: none;
        border-radius: .5rem;
        height: 5vh;
        width: 100%;
    }
</style>