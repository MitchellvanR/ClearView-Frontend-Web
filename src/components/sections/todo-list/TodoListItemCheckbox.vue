<template>
    <label class="checkbox-container" @click="toggleCheckbox">
        <input type="checkbox" v-model="isActiveValue" class="checkbox-input" />
        <span class="checkbox-checkmark"></span>
    </label>
</template>
<script>
export default {
    name: 'TodoListItemCheckbox',
    props: {
        completed: Boolean
    },
    data() {
        return {
            isChecked: false
        }
    },
    methods: {
        toggleCheckbox() {
            this.isChecked = !this.isChecked;
        },
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
        }

        .checkbox-container:hover .checkbox-checkmark {
            background-color: var(--checked-todo-color);
        }

        .checkbox-container .checkbox-input:checked + .checkbox-checkmark {
            background-color: var(--checked-todo-color);
        }
</style>