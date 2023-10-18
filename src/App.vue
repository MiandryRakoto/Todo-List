<template>
  <Todolist />
</template>

<script>
import Todolist from "./views/TodoList"

export default {
  name: 'App',
  components: {
    Todolist
  }
}
</script>

<style>
#app {
  font-family: Poppins;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
