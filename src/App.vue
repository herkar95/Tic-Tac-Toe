<template>
  <div id="app" class="container mx-auto text-center">
    <Header :title="title" :status="status" />
    <div class="game">
      <div class="game-board d-flex justify-content-center">
        <GameBoard :board="board" @turn-passed="turnPassed" />
      </div>
      <div class="game-info">
        <p class="lead mt-2" v-if="turn > 0">Turns passed: {{ turn }}</p>
        <button
          class="btn btn-primary"
          v-if="this.calculateWinner(this.board) || turn > 8"
          @click="resetGame"
        >
          Play again
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header';
import GameBoard from './components/GameBoard';

export default {
  name: 'App',
  components: {
    Header,
    GameBoard,
  },
  data() {
    return {
      title: 'Tic tac toe in Vue.js',
      // represents an empty board with 9 cells
      board: Array(9).fill(null),
      // player X or player O
      player: 'X',
      // X/O's turn, or X/O won the game
      status: null,
      // amount of turns passed in current game
      turn: 0,
    };
  },
  methods: {
    // when a square on the board is clicked
    turnPassed(index) {
      // if the current square has already been clicked (i.e. not null), or if there is a winner
      if (this.board[index] || this.calculateWinner(this.board)) return;
      this.$set(this.board, index, this.player);
      this.turn = ++this.turn;
      const winner = this.calculateWinner(this.board);
      // if there is a winner
      if (winner) this.status = 'Player ' + this.player + ' won!';
      // if turn 9 without a winner (draw)
      else if (this.turn > 8) this.status = 'Game ended in a draw!';
      // if no winner and turns played < 9
      else {
        this.player = this.player === 'X' ? 'O' : 'X';
        this.status = 'Next player: ' + this.player;
      }
    },
    /* checks if a player has won or not
    source - https://reactjs.org/tutorial/tutorial.html#declaring-a-winner */
    calculateWinner(board) {
      const winnerCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let i = 0; i < winnerCombinations.length; i++) {
        const [a, b, c] = winnerCombinations[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return board[a];
        }
      }
      return null;
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.player = 'X';
      this.status = null;
      this.turn = 0;
    },
  },
};
</script>

<style>
/* Global styling */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Lato', Helvetica, sans-serif;
}
</style>
