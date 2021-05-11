<template>

  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <Todo> </Todo> -->
  <Altertodo />

</template>

<script>
// import Todo from './components/Todo.vue'
import Altertodo from './components/Altertodo.vue'

export default {
  name: 'App',
  components: {
    // Todo,
    Altertodo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
