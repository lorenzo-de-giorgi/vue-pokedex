<template>
  <div>
    <PokedexComponent />
    <!-- <SearchComponent /> -->
  </div>
</template>

<script>
import PokedexComponent from './components/PokedexComponent.vue';
import SearchComponent from './components/SearchComponent.vue';

  export default {
    name: 'App',
    components: {
      SearchComponent,
      PokedexComponent
    },
  }
</script>

<style lang="scss" scoped>

</style>