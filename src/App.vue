<template>
  <div id="app">
    <h1>Крестики-Нолики</h1>
    <GameBoard />
  </div>
</template>

<script>
import GameBoard from './components/GameBoard.vue';

export default {
  name: 'App',
  components: {
    GameBoard
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #D4DBE2;
}

h1 {
  margin-top: 30px;
  font-family: "Martian Mono", sans-serif;
  font-size: 1.8rem;
  color: #7B586B;
}

#app {
  text-align: center;
  font-family: 'Arial', sans-serif;
}
</style>
