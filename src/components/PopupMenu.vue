<script setup>
import {ref} from "vue";

const bottom = ref('10%');
const percents = ref(0);

const breakpoints = {
  80: '90%',
  50: '50%',
  20: '10%'
};
const isMoving = ref(false);
function dragStart(e){
  window.addEventListener('pointermove', move);
  window.addEventListener('pointerup', dragEnd)
}

function move(e){
  percents.value = (window.innerHeight - (e.clientY - 40)) / 10;
  bottom.value = window.innerHeight - (e.clientY + 40) + 'px';
}

function dragEnd(e){
  isMoving.value = true;
  window.removeEventListener('pointermove', move);
  bottom.value = Object.entries( breakpoints ).find(([key, value]) => percents.value < key )[1];
  setTimeout(() => isMoving.value = false, 200)
}
</script>

<template>
<div class="menu" @pointerdown="dragStart" :style="{ height: bottom }" :class="{ moving: isMoving  }">
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
  &.moving {
    transition: height 0.2s ease-in-out;
  }
}

.search {
  position: relative;
}

.search-bar {
  position: absolute;
  left: 0;
  right: 0;
  background-color: lightgray;
  border: none;
  padding: 7px;
  border-radius: 5px;
  outline: none;
  color: black;
}

</style>