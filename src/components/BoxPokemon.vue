<template>
    <div class="block-1">
        <p class=""># {{ id }} </p>
        <p class="name">{{ pokemon_name }} </p>
        <div class="block-2">
            <p class="type" v-for="type in pokemon_types" :key="type">
            {{ type.type.name }}
            </p>
        </div>
    </div>
    <img :src="pokemon_image"  class="" alt="">
</template>

<script>
    export default {
        name: "BoxPokemon",
        data()
        {
            return {
                pokemon_image: null,
                pokemon_name: null,
                pokemon_types: null,
                id: null
            }
        },
        props: {
            url_pokemon: String
        },
        methods: {
            async getPokemon() {
                const request = await fetch(`${this.url_pokemon}`)
                const data = await request.json()
                this.pokemon_image =  data.sprites.other.home.front_default
                this.pokemon_name = data.forms[0].name.toUpperCase()
                this.pokemon_types = data.types
                this.id = data.id
            }
        },
        mounted() {
            this.getPokemon()
        }
    }
</script>
<style scoped>

    .name{
        font-weight: bold;
        font-size: 16pt;
    }
    img{
        align-self: flex-end;
        width: 130px;
        height: 130px;
    }
    .block-1{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    .block-2{
        display: flex;
    }
    .type{
        font-size: 13pt;
        color: #f12e2e;
        border-radius: 5px;
        padding: 5px;
        background: #fafafa;
        margin: 2px;
    }
</style>