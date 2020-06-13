<template>
  <span
    @click="$emit('turn-passed')"
    class="square"
    v-bind:class="getCurrentPlayerStyle"
  >{{ value }}</span>
</template>

<script>
export default {
  name: "Square",
  props: {
    row: Number,
    col: Number,
    value: String
  },
  components: {},
  computed: {
    // used to apply different styling to squares depending on if it's X or O playing
    getCurrentPlayerStyle: function() {
      if (this.value === "X") return "square-x";
      else if (this.value === "O") return "square-o";
      return "square-neutral";
    }
  }
};
</script>

<style scoped>
/* styling for all squares */
.square {
  border: 1px solid #999;
  float: left;
  font-size: 2rem;
  font-weight: bold;
  height: var(--square-size);
  text-align: center;
  width: var(--square-size);
  line-height: var(--square-size);
  color: #fff;
  transition: 0.2s ease;
  margin: 1px;
  cursor: pointer;
}
/* styling for squares before they are pressed*/
.square-neutral {
  background: var(--primary-blue);
}
.square-neutral:hover {
  background: var(--secondary-blue);
}
/* styling for squares pressed by player X */
.square-x,
square-x:hover {
  background: var(--player-x);
}
/* styling for squares pressed by player O */
.square-o,
square-o:hover {
  background: var(--player-o);
}
/* on small screens */
@media screen and (max-width: 430px) {
  .square {
    width: var(--square-size-small);
    line-height: var(--square-size-small);
    height: var(--square-size-small);
  }
}
</style>
