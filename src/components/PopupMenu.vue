<script setup>
import {ref} from "vue";

const bottom = ref('3%');
const percents = ref(0);

const breakpoints = {
  80: '90%',
  50: '50%',
  20: '3%'
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

const tabs = ref([
  {name: 'Все'},
  {name: 'Места'},
  {name: 'Скидки'},
  {name: 'Карты'},
]);

const selectedTabIndex = ref(0);
</script>

<template>
<div class="menu" @pointerdown="dragStart" :style="{ height: bottom }" :class="{ moving: isMoving  }">
  <div class="search">
    <input type="text" class="search-bar" placeholder="Поиск мест, скидок, карт поблизости" @focus="bottom = breakpoints['80']" />
  </div>
  <div class="tabs">
    <div v-for="(tab, index) in tabs" @click="selectedTabIndex = index" class="tab" :key="tab.name" :class="{ selected: index === selectedTabIndex }">{{ tab.name }}</div>
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
  height: 40px;
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

.tabs {
  color: black;
  display: flex;
  justify-content: space-around;
  gap: 5px;
  .tab {
    width: 100%;
    padding-bottom: 5px;
    &.selected {
      color: green;
      border-bottom: green solid 1px;
    }
  }
}
</style>