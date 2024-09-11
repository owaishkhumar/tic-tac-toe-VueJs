<template>
  <div id="app">
    <TicTacToe />
  </div>
</template>

<script>
import TicTacToe from './components/TicTacToe.vue'

export default {
  name: 'App',
  components: {
    TicTacToe
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>