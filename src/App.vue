<template>
  <TodoPage />
</template>

<script>
import TodoPage from './components/layout/page-containers/TodoPage.vue';

export default {
  name: 'App',
  components: {
    TodoPage
  }
}
</script>

<style>
:root {
  --primary-color: #D7EEEC;
  --secondary-color: #D5E3E1;
  --tertiary-color: #E7E4DF;
  --add-button-color: #3C7669;
  --save-button-color: #52AB9F;
  --delete-button-color: #C34F5D; 
}

* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 1.5rem;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
