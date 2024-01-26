<template>
    <div class="todo-title-details">
        <h2><label for="title-box">Title: </label></h2>
        <input id="title-box" name="title-box" type="text" value="">
    </div>
</template>
<script>
export default {

}
</script>
<style>
    .todo-title-details {
        display: flex;
        flex-direction: column;
        text-align: left;
        gap: 1rem;
        margin-top: 20vh;
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