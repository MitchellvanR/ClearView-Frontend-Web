<template>
    <div class="user-profile">
        <img class="logo" src="@/assets/logo.png" alt="ClearView logo">
        <div class="text">
            <h2>ClearView</h2>
            <p>Clear view, clear mind</p>
        </div>
    </div>
</template>
<script>
export default {

}
</script>
<style scoped>
    .user-profile {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .logo {
        max-width: 50%;
        max-height: 50%;
        margin-right: 5%;
    }

    .text {
        display: flex;
        flex-direction: column;
        text-align: left;
    }
</style>