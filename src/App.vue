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
  --add-button-hover-color: #4b9282;
  --save-button-color: #52AB9F;
  --delete-button-color: #C34F5D; 
  --checked-todo-color: #7BC9BF;
  --checkbox-hover-color: #ECF6FF;
  --exit-button-background-color: #ECECEC;
  --exit-button-text-color: #C1C1C1;
  --default-text-color: #ffffff;
}

* {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

#app {
  font-size: 1.7vh;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
