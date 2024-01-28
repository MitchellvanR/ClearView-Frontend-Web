<template>
    <BaseModal @modal-close="handleModalClose">
        <div class="add-todo-list-modal-content">
            <h2>Add todo list modal</h2>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean lacinia mauris mi, sed posuere sem finibus ac. Suspendisse potenti. Phasellus velit justo, laoreet id lorem vitae, lobortis lacinia metus. Aenean fringilla ipsum id tortor maximus egestas. Praesent porta tincidunt odio, at dignissim justo placerat vel. In sagittis eget nisi eu auctor. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Donec sit amet vulputate mi. Phasellus egestas, mi in pellentesque eleifend, tortor massa molestie neque, non viverra urna odio ut felis. Pellentesque sit amet felis sapien. Mauris sollicitudin hendrerit nulla, in pharetra erat sagittis id. Maecenas ullamcorper, urna ac pharetra auctor, mi nunc hendrerit elit, et ultricies leo ligula suscipit lorem. Suspendisse ac diam eget urna mattis aliquet. Morbi dictum, ex non dictum aliquam, lacus metus auctor eros, ac egestas dui est in erat.</p>
        </div>
    </BaseModal>
</template>
<script>
import BaseModal from './BaseModal.vue'

export default {
    name: 'AddTodoListModal',
    components: {
        BaseModal
    },
    methods: {
        handleModalClose() {
            this.$emit('modal-close')
        }
    }
}
</script>
<style>
    .add-todo-list-modal-content {
        height: 80%;
    }
</style>