<script setup>
  import PopupMenu from "./components/PopupMenu.vue";

  const map = new Microsoft.Maps.Map('#map');
</script>

<template>
  <div>
    <PopupMenu />
  </div>
</template>

<style scoped>
</style>

<style>
input[type=text] {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

* {
  margin: 0;
  padding: 0;
  outline: 0;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
</style>
