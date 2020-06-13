<template>
  <div id="app" class="container mx-auto text-center">
    <Header :title="title" />
    <GameBoard :board="board" @turn-passed="turnPassed" />
    <GameInfo :status="status" :turn="turn" :winner="winner" @reset-game="resetGame" />
  </div>
</template>

<script>
import Header from "./components/Header";
import GameBoard from "./components/GameBoard";
import GameInfo from "./components/GameInfo";

export default {
  name: "App",
  components: {
    Header,
    GameBoard,
    GameInfo
  },
  data() {
    return {
      // heading above the game board
      title: "Tic tac toe in Vue.js",
      // represents an empty board with 9 cells
      board: Array(9).fill(null),
      // player X or player O (whose turn it is)
      player: "X",
      // game status (X/O's turn, or X/O won the game)
      status: null,
      // amount of turns passed in current game
      turn: 0,
      // set to true if someone wins
      winner: false
    };
  },
  methods: {
    // when a square on the board is clicked
    turnPassed(index) {
      // if the current square has already been clicked (i.e. not null), or if there is a winner
      if (this.board[index] || this.calculateWinner(this.board)) return;

      this.$set(this.board, index, this.player); // set value of square to X or O
      this.turn = ++this.turn;
      this.winner = this.calculateWinner(this.board);

      // if there is a winner
      if (this.winner) this.status = "Player " + this.player + " wins!";
      // if turn 9 without a winner (draw)
      else if (this.turn > 8) this.status = "Game ended in a draw!";
      // if no winner and turns played < 9 (continue playing)
      else {
        this.player = this.player === "X" ? "O" : "X";
        this.status = "Next player: " + this.player;
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
        [2, 4, 6]
      ];
      for (let i = 0; i < winnerCombinations.length; i++) {
        const [a, b, c] = winnerCombinations[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return true;
        }
      }
      return false;
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.player = "X";
      this.status = null;
      this.turn = 0;
      this.winner = false;
    }
  }
};
</script>

<style>
/* Global styling */
:root {
  --square-size: 8rem;
  --square-size-small: 6rem;
  --primary-blue: #14579c;
  --secondary-blue: #0085ff;
  --player-x: #19a0ff;
  --player-o: #002742;
  --primary-orange: #ff861d;
  --secondary-orange: #d66300;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Lato", Helvetica, sans-serif;
}
</style>
