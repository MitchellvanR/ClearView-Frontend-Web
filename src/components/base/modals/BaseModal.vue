<template>
    <div class="modal">
        <div class="modal-inner">
            <div class="modal-close-button-wrapper">
                <button class="modal-close" @click="handleModalClose">X</button>
            </div>
            <slot class="modal-content"></slot>
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
        padding: 1rem;
        padding-bottom: 4rem;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .modal-content {
        height: 80%;
    }

    .modal-close-button-wrapper {
        height: 10%;
        display: flex;
        align-items: flex-start;
        justify-content: flex-end;
        width: 100%;
    }

    .modal-close {
        background-color: var(--exit-button-background-color);
        border-radius: 50%;
        border: none;
        font-size: 1.5vw;
        margin-top: 1vh;
        margin-right: 2vh;
        color: var(--exit-button-text-color);
        width: 2.5vw;
        height: 2.5vw;
        transition: all .3s ease;
    }

    .modal-close:hover {
        cursor: pointer;
        background-color: var(--exit-button-text-color);
        color: var(--exit-button-background-color);
        transition: all .3s ease;
    }
</style>