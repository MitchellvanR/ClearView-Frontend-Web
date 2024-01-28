<template>
    <div class="modal">
        <div class="modal-inner">
            <slot class="modal-content"></slot>
            <div class="modal-close-button-wrapper">
                <button class="modal-close" @click="handleModalClose">Close</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'BaseModal',
    methods: {
        handleModalClose() {
            this.$emit('modal-close')
        }
    }
}
</script>
<style scoped>
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 99;
        background-color: rgba(0, 0, 0, 0.2);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal-inner {
        background-color: white;
        border-radius: .5rem;
        width: 80vw;
        height: 50vh;
        padding: 4rem;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .modal-content {
        height: 80%;
    }

    .modal-close-button-wrapper {
        height: 20%;
        display: flex;
        align-items: flex-end;
    }

    .modal-close {
        display: block;
        font-size: 1.7vh;
        border: none;
        border-radius: .5rem;
        background-color: var(--delete-button-color);
        color: var(--default-text-color);
        width: 5vw;
        height: 4vh;
        transition: all .2s ease;
    }

    .modal-close:hover {
        cursor: pointer;
        background-color: var(--delete-button-hover-color);
        transition: all .2s ease;
    }
</style>