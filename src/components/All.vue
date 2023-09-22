<script setup>
const items = [
  {
    header: 'Московский Ювелирный Завод',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Пятерочка',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Связной',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Связной',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Связной',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Связной',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  },
  {
    header: 'Московский Ювелирный Завод',
    description: 'Москва, Павелецкая площадь, 2с1 (958 км)',
  }
]
</script>

<template>
  <div>
    <p class="tab-header">Места поблизости</p>
  </div>
  <div>
    <div v-for="item in items" :key="item.header" class="company-item">
      <div>
        <img alt="Company logo" src="src/assets/vue.svg" />
      </div>
      <div>
        <p class="tab-header">{{ item.header }}</p>
        <p class="company-desc">{{ item.description }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.tab-header {
  text-align: left;
  font-weight: bolder;
}

.company-desc {
  text-align: left;
}

.company-item {
  display: flex;
  margin: 10px 0;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
</style>