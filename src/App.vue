<template>
  <div id="app">
    <TodoApp msg="Todo Vue.js App" />
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp,
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@100;300;400;500;600;700&family=Open+Sans:wght@300;400;500;600&family=Roboto:wght@500;600;700&display=swap');

*,
*:after,
*:before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
  list-style-type: none;
}

@media (max-width: 600px) {
  * {
    width: 90vw;
  }
}

html,
body {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  background-color: #f2f1f1;

  font-size: 62.5%;
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

#app {
  font-size: 12px;
  display: grid;
  place-items: center;
}

input,
textarea,
select {
  height: 3.4rem;
  border: 1.5px rgb(173, 173, 173) solid;
  border-radius: 5px;
  padding-left: 15px;

  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
input:focus,
textarea:focus,
select:focus {
  outline: none;
}
</style>
