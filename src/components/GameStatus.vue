<template>
  <div class="status">
    <div v-if="winner" class="winner">
      Победитель: {{ winner }}
    </div>
    <div v-else-if="isDraw" class="draw">
      Ничья!
    </div>
    <div v-else>
      Текущий игрок: {{ currentPlayer }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameStatus',
  props: {
    winner: String,
    isDraw: Boolean,
    currentPlayer: String
  }
};
</script>

<style scoped>
.status {
  font-family: "Martian Mono", sans-serif;
  font-size: 1.3rem;
  letter-spacing: 0.005rem;
}
.winner {
  color: #597A58;
  font-weight: bold;
}
.draw {
  color: #3B3136;
  font-weight: bold;
}
</style>
