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
</style>
