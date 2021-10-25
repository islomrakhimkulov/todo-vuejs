<template>
  <div class="container">
    <img alt="Vue logo" src="./assets/logo.png">
    <todo-list v-model="todos" />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList,
  },
  data: () => ({
    todos: [
      {text:'Reading a book', id: '1', isComplete: false},
      {text:'Listening ESL podcasts', id: '2', isComplete: false},
      {text:'I have to memorize new words', id: '3', isComplete: false},
    ],
  }),
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

body {
  height: 100%; 
  background-image: linear-gradient(62deg, rgba(7, 86, 160, 0.973) 13%,rgba(255,122,151,0.5) 4%),
                    linear-gradient(44deg, rgba(0, 43, 99, 0.079) 39%,rgba(242,140,143,0.5) 18%),
                    linear-gradient(18deg, rgba(84,202,242,0.031) 40%,rgba(247,155,187,0.5) 54%),
                    linear-gradient(58deg, rgba(90,90,237,0.161) 83%,rgba(249,156,142,0.5) 34%);
                    background-blend-mode: normal,lighten multiply,hard-light;
                    /* overflow: hidden; */
}
</style> 
