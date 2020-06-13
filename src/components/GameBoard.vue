<template>
  <div class="game">
    <div class="game-board d-flex justify-content-center">
      <div class="squares shadow">
        <!--creates three rows -->
        <div class="row" v-for="row in 3" :key="row">
          <!--creates three squares per row -->
          <div class="sq" v-for="col in 3" :key="col">
            <Square
              :row="row"
              :col="col"
              :value="board[calculateRowIndex(col, row)]"
              @turn-passed="$emit('turn-passed', calculateRowIndex(col, row))"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Square from "./Square";
export default {
  name: "GameBoard",
  props: {
    board: Array
  },
  components: {
    Square
  },
  methods: {
    // calculates the index of the clicked square
    calculateRowIndex(col, row) {
      const maxRows = 3;
      return row * maxRows + col - (maxRows + 1);
    }
  }
};
</script>

<style scoped></style>
