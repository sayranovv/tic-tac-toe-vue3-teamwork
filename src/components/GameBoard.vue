<template>
  <div>
    <div class="game-container">

    <div class="game-status">
    </div>
    <div class="board">
        <div class="row" v-for="(row, rowIndex) in board" :key="rowIndex">
          <div class="cell" v-for="(cell, colIndex) in row" :key="colIndex" @click="makeMove(rowIndex, colIndex)">
            {{ cell }}
          </div>
        </div>
      </div>
    <button @click="resetGame">Начать новую игру</button>
    </div>

  </div>
</template>

<script>

export default {
  name: 'GameBoard',
  components: {
    GameStatus
  },
  data() {
    return {
      board: [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ],
      currentPlayer: 'X',
      winner: null,
      isDraw: false
    };
  },
  methods: {
    makeMove(rowIndex, colIndex) {
      // Если клетка уже занята или игра закончена, не выполнять ход
      if (this.board[rowIndex][colIndex] !== '' || this.winner || this.isDraw) {
        return;
      }
      // Помечаем клетку текущим игроком
      this.board[rowIndex][colIndex] = this.currentPlayer;
      // Проверяем победу
      this.checkWinner();
      // Меняем игрока
      this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
    },
    checkWinner() {
      // Проверка всех возможных вариантов победы
      for (let i = 0; i < 3; i++) {
        if (
            this.board[i][0] !== '' &&
            this.board[i][0] === this.board[i][1] &&
            this.board[i][1] === this.board[i][2]
        ) {
          this.winner = this.board[i][0];
          return;
        }
        if (
            this.board[0][i] !== '' &&
            this.board[0][i] === this.board[1][i] &&
            this.board[1][i] === this.board[2][i]
        ) {
          this.winner = this.board[0][i];
          return;
        }
      }
      if (
          this.board[0][0] !== '' &&
          this.board[0][0] === this.board[1][1] &&
          this.board[1][1] === this.board[2][2]
      ) {
        this.winner = this.board[0][0];
        return;
      }
      if (
          this.board[0][2] !== '' &&
          this.board[0][2] === this.board[1][1] &&
          this.board[1][1] === this.board[2][0]
      ) {
        this.winner = this.board[0][2];
        return;
      }
      // Проверка ничьей
      if (!this.board.flat().includes('')) {
        this.isDraw = true;
      }
    },
    resetGame() {
      // Сброс игры
      this.board = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ];
      this.currentPlayer = 'X';
      this.winner = null;
      this.isDraw = false;
    }
  }
};
</script>

<style scoped>
</style>
