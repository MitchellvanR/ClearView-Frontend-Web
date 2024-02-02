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
  --primary-color: #C4E9F2;
  --secondary-color: #66A9AA;
  --tertiary-color: #FDF1DA;
  --add-button-color: #3C7669;
  --add-button-hover-color: #4b9282;
  --save-button-color: #52AB9F;
  --delete-button-color: #C34F5D; 
  --delete-button-hover-color: #C66D77;
  --checked-todo-color: #7BC9BF;
  --checkbox-hover-color: #ECF6FF;
  --exit-button-background-color: #ECECEC;
  --exit-button-text-color: #C1C1C1;
  --default-text-color: #2c3e50;
  --dark-background-text-color: #FFFFFF;
  --input-offwhite-color: #EEEEEE;
}

* {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

*::-webkit-scrollbar {
    width: .5rem;
}

*::-webkit-scrollbar-track {
    background-color: rgba(255, 255, 255, 0);
    z-index: -99;
}

*::-webkit-scrollbar-thumb {
    background-color: var(--add-button-color);
    border-radius: 16px;
}

*::-webkit-scrollbar-button {
    display:none;
}

#app {
  font-size: 1.7vh;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--default-text-color);
}
</style>
