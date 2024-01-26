<template>
    <div class="todo-description-details">
        <h2><label for="description-box">Description: </label></h2>
        <textarea id="description-box" name="description-box" rows="7" :value="descriptionValue"></textarea>
    </div>
</template>
<script>
export default {
    name: 'TodoDescriptionDetails',
    props: {
        descriptionValue: String
    }
}
</script>
<style>
    .todo-description-details {
        display: flex;
        flex-direction: column;
        text-align: left;
        gap: 1rem;
        width: 75%;
    }

    #description-box {
        width: 100%;
        resize: none;

        font-size: 100%;
        box-sizing: border-box;
        padding: 1rem;
        border: none;
        border-radius: .5rem;
    }
</style>