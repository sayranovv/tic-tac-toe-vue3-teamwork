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
</style>
