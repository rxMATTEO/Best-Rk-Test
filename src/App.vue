<script setup>
  const map = new Microsoft.Maps.Map('#myMap');
</script>

<template>
  <div>
    <div id="myMap" style="position:relative;width:600px;height:400px;" />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
