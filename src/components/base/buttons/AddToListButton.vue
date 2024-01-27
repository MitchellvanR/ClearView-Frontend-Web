<template>
    <div class="add-to-list-button-wrapper">
        <button class="add-to-list-button" @click="startModal">Add</button>
    </div>
</template>
<script>
export default {
    name: 'AddToListButton',
    methods: {
        startModal() {
            console.log('Starting modal...')
        }
    }
}
</script>
<style>
    .add-to-list-button-wrapper {
        display: flex;
        justify-content: center;
    }

    .add-to-list-button {
        display: block;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--add-button-color);
        color: var(--default-text-color);
        width: 10vw;
        height: 5vh;
        transition: all .2s ease;
    }

    .add-to-list-button:hover {
        cursor: pointer;
        background-color: var(--add-button-hover-color);
        transition: all .2s ease;
    }
</style>