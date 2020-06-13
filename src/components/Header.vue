<template>
  <div class="header p-4">
    <div class="row justify-content-center">
      <span class="col-12">
        <img src="../assets/header-logo.png" alt="Logo" title="Logo" class="logo" />
      </span>
      <h1 class="align-self-center mt-4 display-4">Tic Tac Toe in Vue.js</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String
  }
};
</script>

<style scoped></style>
