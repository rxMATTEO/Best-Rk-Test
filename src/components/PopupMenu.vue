<script setup>
import {ref} from "vue";

const bottom = ref(0);
function dragStart(e){
  window.addEventListener('pointermove', move);
  window.addEventListener('pointerup', dragEnd)
}

function move(e){
  bottom.value = window.innerHeight - e.clientY - 40;
}

function dragEnd(e){
  window.removeEventListener('pointermove', move);
}
</script>

<template>
<div class="menu" @pointerdown="dragStart" :style="{ bottom: bottom + 'px' }">
  <div class="search">
    <input type="text" class="search-bar" placeholder="Поиск мест, скидок, карт поблизости" />
  </div>
</div>
</template>

<style scoped lang="scss">
.menu {
  position: absolute;
  z-index: 1000;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  padding: 15px 5px;
  height: 5%;
  touch-action: none;
}

.search {
  position: relative;
}

.search-bar {
  position: absolute;
  left: 0px;
  right: 0px;
  background-color: lightgray;
  border: none;
  padding: 7px;
  border-radius: 5px;
  outline: none;
  color: black;
}

</style>