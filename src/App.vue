<template>
 
  <div id="app">


    <div class="column is-half is-offset-one-quarter">

      <h1  class="title is-1" >Pokedex</h1>

      <input class="input is-rounded" :v-model="busca" type="text" placeholder="Buscar Pokémon">
      <button class="button is-success" @click="buscar" >Buscar</button>

      <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
      
      <Pokemon :name="pokemon.name" :numero="index + 1" :url="pokemon.url" />
    </div>


    </div>
    



  </div>

</template>

<script>
import axios from "axios"
import Pokemon from "./components/VuePokemon.vue"

export default {

  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },

  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0")
        .then((pokemons)=>{
          console.log(pokemons.data.results);
          this.pokemons = pokemons.data.results;
          this.filteredPokemons = pokemons.data.results
        })
        .catch((msgErro)=>{
          console.log('Erro ao carregar os pokemons ' + msgErro)
        })

  },
  

  components:{
    Pokemon
  },

  methods:{

    buscar:function(){

        this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemons => pokemons.name == this.busca)
      }
    }

  },

  
  
}
</script>

<style>

  #app{
    margin: 0 auto;
    text-align: center;
  }

  .is-success{
    margin-top: 8px;
  }

</style>
