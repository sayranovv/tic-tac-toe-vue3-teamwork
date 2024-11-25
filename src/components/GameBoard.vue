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
.game-container {
  display: flex;
  flex-direction: column; /* размещаем элементы по вертикали */
  align-items: center; /* выравниваем по горизонтали */
  height: 100vh; /* растягиваем контейнер на всю высоту экрана */
  text-align: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
  gap: 10px;
  margin: 20px 0;
}

.cell {
  font-family: "Martian Mono", sans-serif;
  margin-top: 10px;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  border: 2px solid #7B586B;
  cursor: pointer;
  border-radius: 10px;
  color: #453C41;
}

button {
  font-family: "Martian Mono", sans-serif;
  letter-spacing: 0.005rem;
  font-size: 0.9rem;
  margin-top: 30px;
  padding: 10px 20px;
  background-color: #7B586B;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 10px;
}

button:hover {
  background-color: #453C41;
}
</style>
