<template>
  <span @click="$emit('turn-passed')" class="square">{{ value }}</span>
</template>

<script>
export default {
  name: 'Square',
  props: {
    row: Number,
    col: Number,
    value: String,
  },
  components: {},
};
</script>

<style>
:root {
  --square-size: 8rem;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 2rem;
  font-weight: bold;
  height: var(--square-size);
  text-align: center;
  width: var(--square-size);
  line-height: var(--square-size);
}
</style>
