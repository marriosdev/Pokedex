<template>
  <div>
    <router-link to="/">
      <span class="button-back">
        <img src="http://pngimg.com/uploads/pokeball/pokeball_PNG19.png" alt="">
        <p>VOLTAR</p>
      </span>
    </router-link>
  </div>
  <div class="pokemon">
    <div class="poke-info">
      <h1 class="name">{{ name }} </h1>
      <img :src="image" alt="">
    </div>
    <div class="stats">
      <div v-for="stat in pokemon" :key="stat">
        <Graficos :tamanho="stat.base_stat" :nome="stat.stat.name" />
      </div> 
    </div>
    </div>
</template>

<script>
import Graficos from '../components/Graficos.vue'
export default {
  name: 'Pokemon',
  data() {
    return {
      pokemon: null,
      image: null,
      name: null
    }
  },
  components: {
    Graficos
  },
  methods: {
    async getPokemon() {
      const request = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.$route.query.name}`)
      const data = await request.json()
      this.image = data.sprites.other.home.front_default
      this.name = data.name
      console.log(this.image)
      this.pokemon = data.stats
    }
  },
  mounted() {
    this.getPokemon()
  }
}
</script>

<style scoped>
  a{
    text-decoration: none;
  }
  .button-back{
    justify-content: space-around;
    width: 120px;
    align-items: center;
    display: flex;
    color: #ffffff;
    padding: 5px;
    border-radius: 3px;
    background: #ff2d2d;
    margin: 10px;
  }
  .button-back img{
    height: 30px;
  }
  .poke-info{
    text-align: center;
    margin-bottom: 30px;

  }
  .pokemon{  
    margin-top: 50px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  img{
    height: 240px;
  }
  h1{
    text-transform: uppercase;
  }
  @media screen and (max-width: 600px){
    .pokemon{
      flex-direction: columns;
    }
  }
</style>