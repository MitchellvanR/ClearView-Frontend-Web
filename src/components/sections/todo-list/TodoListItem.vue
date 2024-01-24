<template>
    <div 
        class="todo-list-item"
        :class="{ active: isActiveValue }"
        @mouseover="handleMouseOver"
        @mouseout="handleMouseOut"
    >
        <TodoListItemCheckbox />
        <li class="todo-list-item-element">{{ todo.title }}</li>
    </div>
</template>
<script>
import TodoListItemCheckbox from './TodoListItemCheckbox.vue'

export default {
    name: 'TodoListItem',
    components: {
        TodoListItemCheckbox
    },
    props: {
        todo: Object,
        isActive: Boolean
    },
    data() {
        return {
            isActiveValue: this.isActive,
            isHovered: false,
            isTransitioning: false
        }
    },
    watch: {
        isActive: function(newValue) {
            this.isActiveValue = newValue;
        },
    },
    methods: {
        handleMouseOver() {
            this.isHovered = true;
            this.isTransitioning = true;
        },
        handleMouseOut() {
            this.isTransitioning = false;
        },
        handleTransitionEnd() {
            if (!this.isTransitioning) {
            this.isHovered = false;
            }
        }
    }
}
</script>
<style scoped>
    .todo-list-item {
        border-radius: 2rem 0 0 2rem;
        display: flex;
        flex-direction: row;
        padding: 1rem 1rem 1rem 2rem;
        /* padding-left: 0; */
        transition: background-color 0.2s ease;
    }

    .todo-list-item:hover, .active {
        background-color: var(--tertiary-color);
        cursor: pointer;
    }

    .hover {
        transition: background-color 0.2s ease;
    }

    .todo-list-item-element {
        list-style: none;
        margin-left: 5%;
    }
</style>