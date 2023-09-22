<script setup>
import {ref, shallowReactive, shallowRef} from "vue";
import All from "./All.vue";
import Places from "./Places.vue";
import Sales from "./Sales.vue";
import Maps from "./Maps.vue";

const percents = ref(0);

const breakpoints = {
  80: '90%',
  50: '50%',
  20: '8%'
};
const bottom = ref(breakpoints["20"]);
const isMoving = ref(false);
function dragStart(e){
  window.addEventListener('pointermove', move);
  window.addEventListener('pointerup', () => dragEnd())
}

function move(e){
  percents.value = (window.innerHeight - (e.clientY - 40)) / 10;
  bottom.value = window.innerHeight - (e.clientY + 40) + 'px';
}

function dragEnd(bottomValue){
  isMoving.value = true;
  console.log(bottomValue)
  window.removeEventListener('pointermove', move);
  bottom.value = bottomValue || Object.entries( breakpoints ).find(([key, value]) => percents.value < key )[1];
  setTimeout(() => isMoving.value = false, 200)
}

const tabs = shallowRef([
  {
    name: 'Все',
    component: All,
  },
  {
    name: 'Места',
    component: Places,
  },
  {
    name: 'Скидки',
    component: Sales,
  },
  {
    name: 'Карты',
    component: Maps
  },
]);

function stickTab(e){
  const element = e.target;
  if(element.scrollTop + element.offsetHeight>= element.scrollHeight) {
    dragEnd(breakpoints['80'])
  }
  else if(element.scrollTop === 0){
    dragEnd(breakpoints['50'])
  }
}
const selectedTabIndex = ref(0);
</script>

<template>
<div class="menu" :style="{ height: bottom }" :class="{ moving: isMoving  }">
  <div class="grabber" @pointerdown="dragStart">
    <div class="grabber-icon" />
  </div>
  <div class="search">
    <input type="text" class="search-bar" placeholder="Поиск мест, скидок, карт поблизости" @focus="bottom = breakpoints['80']" />
  </div>
  <div class="tabs">
    <div v-for="(tab, index) in tabs" @click="selectedTabIndex = index" class="tab" :key="tab.name" :class="{ selected: index === selectedTabIndex }">{{ tab.name }}</div>
  </div>
  <div class="dynamic-tab-content" @scroll="stickTab">
    <component :is="tabs[selectedTabIndex].component" />
  </div>
</div>
</template>

<style scoped lang="scss">
$primary: #4BC6A6;

.menu {
  position: absolute;
  z-index: 1000;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  padding: 5px 5px;
  height: 10%;
  touch-action: none;
  overflow: hidden;
  &.moving {
    transition: height 0.2s ease-in-out;
  }
  .grabber {
    padding: 2px 0;
    .grabber-icon {
      background: gray;
      height: 5px;
      margin-bottom: 5px;
      width: 50px;
      display: inline-block;
      text-align: center;
      border-radius: 5px;
      background: $primary;
    }
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
  position: absolute;
  right: 0;
  left: 0;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  .tab {
    width: 100%;
    padding-bottom: 5px;
    &.selected {
      color: $primary;
      border-bottom: $primary solid 1px;
    }
  }
}

.dynamic-tab-content {
  margin-top: 35px;
  color: black;
  max-height: 75%;
  overflow-y: scroll;
}
</style>