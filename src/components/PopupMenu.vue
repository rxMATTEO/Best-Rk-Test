<script setup>
import {ref} from "vue";

const bottom = ref(0);
const percents = ref(0);

const breakpoints = {
  80: '100%',
  50: '50%',
  20: '20%'
};
function dragStart(e){
  window.addEventListener('pointermove', move);
  window.addEventListener('pointerup', dragEnd)
}

function move(e){
  percents.value = (window.innerHeight - (e.clientY - 40)) / 10;
  bottom.value = window.innerHeight - (e.clientY + 40) + 'px';
}

function dragEnd(e){
  window.removeEventListener('pointermove', move);
  console.log(Object.entries( breakpoints ).find(([key, value]) => percents.value < key )[1] )
  bottom.value = Object.entries( breakpoints ).find(([key, value]) => percents.value < key )[1];
}
</script>

<template>
<div class="menu" @pointerdown="dragStart" :style="{ height: bottom }">
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
  height: 10%;
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