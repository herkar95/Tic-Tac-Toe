<template>
  <div class="game-info">
    <span class="lead my-2 py-2" v-if="status">{{ status }}</span>
    <span class="lead my-2 py-2" v-if="turn > 0">Turns passed: {{ turn }}</span>
    <button class="btn w-50 my-2" v-if="winner || turn > 8" @click="$emit('reset-game')">Play again</button>
  </div>
</template>

<script>
export default {
  name: "GameInfo",
  props: {
    status: String,
    turn: Number,
    winner: Boolean
  }
};
</script>

<style scoped>
span {
  border-bottom: 1px solid var(--primary-blue);
  display: block;
  font-size: 1.5rem;
}
.btn {
  background: var(--primary-blue);
  color: #fff;
  transition: 0.2s ease;
  font-weight: lighter;
  height: 3rem;
  font-size: 1.5rem;
}
.btn:hover {
  background: var(--secondary-blue);
  color: #fff;
  text-decoration: underline;
}
</style>