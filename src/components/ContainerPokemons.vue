<template>
    <div class="search">
        <img src="https://icones.pro/wp-content/uploads/2021/06/icone-loupe-rouge.png" alt="">
        <input type="text" @input="searchPoke" v-model="searchName" placeholder="Busque um pokémon">
        <img src="https://cdn-icons-png.flaticon.com/512/528/528101.png" alt="pokebola">
    </div>
    <div v-show="noResults" class="noresult">
        <h2>Nenhum resultado para "{{ searchName }}"</h2>
        <img src="http://67.media.tumblr.com/a47e7b8d91ea384ca51bfc87801d50c5/tumblr_oa5tfrPJYd1qb0pfbo1_500.gif" alt="nenhum resultado">
    </div>
    <div  id="container-pokemons">
        <!-- <><button>Ver</button></a> -->
        <router-link :to="'/pokemon?name='+pokemon.name"  class="box" v-for="pokemon in list_pokemons" v-bind:key="pokemon">
            <BoxPokemon :url_pokemon="pokemon.url" /> 
        </router-link>
    </div>    
    <button @click="moreResults" v-if="searchOff">Mostrar mais</button>
</template>

<script>
    import BoxPokemon from './BoxPokemon.vue'

    export default {
        name: "ContainerPokemons",
        data(){
            return {
                list_all_poke: [],
                list_pokemons: [],
                offset: 0,
                searchName: "",
                searchOff: true,
                noResults: false
            }
        },
        components: {
            BoxPokemon
        },
        methods: {
            
            /**
             * 
             */
            async getAll() {
                const request = await fetch(`https://pokeapi.co/api/v2/pokemon?offset=0&limit=1118`)
                const data = await request.json()
                this.list_all_poke = this.list_pokemons.concat(data.results) 
            },

            /**
             * 
             */
            async updateList(newList) {
                this.list_pokemons  = newList
            },

            /*  
            List Pokemons
            */
            async getPokemons(){
                const request = await fetch(`https://pokeapi.co/api/v2/pokemon?offset=${this.offset}&limit=8`)
                const data = await request.json()
                this.list_pokemons = this.list_pokemons.concat(data.results) 
            },

            /*
            Get more results
            */
            async moreResults(){
                this.offset += 8
                this.getPokemons()
            },

            /**
             * 
             */
            async searchPoke() {
                this.searchOff = false

                if(this.searchName == "") {
                    this.searchOff = true
                    this.offset = 0
                    this.list_pokemons = []
                    this.getPokemons()
                    return true
                }

                let newList = [] 
                this.list_pokemons = []
                const strin = this.searchName
                let count = 0

                this.list_all_poke.forEach(function(obj) {
                    if (obj.name.search(strin) != -1) {
                        if(count < 15) {
                            newList = newList.concat(obj)
                            count ++
                        }
                    }
                })

                this.updateList(newList)

                if(newList.length == 0) {
                    this.noResults = true
                }else{
                    this.noResults = false
                    this.searchOn = false
                }
            }
        },
        mounted(){
            this.getAll()
            this.getPokemons()
        },
    }
</script>

<style scoped>
    a{
        text-decoration: none;        
    }
    #container-pokemons{
        width: 100%;
        align-self: center;
        justify-content: flex-start;
        display: flex;
        flex-wrap: wrap;
    }
    .box{
        color: white;
        background: #ff3131;
        margin-bottom: 40px !important;
        height: 150px;
        border-radius: 10px;
        padding: 10px;
        justify-content: space-between;
        display: flex;
        margin: 10px;
        width:47%;
    }
    button{
        font-weight: bold;
        border-radius: 10px;
        padding: 15px;
        margin: 20px;
        font-size: 14pt;
        width: 100%;
        align-self: center;
        max-width: 400px;
        background: #ff3131;
        color: #ffffff;
        border: 3px solid #ff3131;
        cursor: pointer;
        transition: 300ms;
    }
    button:hover{
        background: #ffffff;
        color: #ff3131;
        border: 3px solid #ff3131;
        cursor: pointer;
    }
    .search img{
        height: 100%;
    }
    .search input{
        outline: none;
        border: none;
        width: 100%;
        margin-left: 8px;
        font-size: 16pt;
    }
    .search{
        position: sticky;
        margin-bottom: 60px;
        height: 60px;
        display: flex;
        border: 2px solid rgb(250, 59, 59);
        border-radius: 10px;
        outline-offset: 0pt;
        outline-color: rgb(0, 140, 255);
        padding: 5px;
        margin: 0 10%;
    }
    .noresult {
        justify-self: center;
        align-self: center;
        text-align: center;        
        margin-top: 50px;
    }
    .noresult img{
        width: 200px !important;
    }
    @media screen and (max-width: 860px){
        .box{
            width: 100% !important;
        }
    }
    @media screen and (min-width: 900px){
        #container-pokemons{
            justify-content: center;
            width: 900px;
        }
    }
</style>