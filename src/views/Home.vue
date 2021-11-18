<template>
  <div class="home">
      <ContainerPokemons />
  </div>
</template>

<script>
  import ContainerPokemons from '../components/ContainerPokemons.vue'
  export default {
    name: 'Home',
    components: {
      ContainerPokemons
    }
  }
</script>
<style scoped>
  .home{
    display: flex;
    flex-direction: column;
  }
  
</style>