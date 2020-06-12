<template>
  <div class="header">
    <h1>{{ title }}</h1>
    <h3 v-if="status">{{ status }}</h3>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String,
    status: String,
  },
};
</script>

<style scoped></style>
