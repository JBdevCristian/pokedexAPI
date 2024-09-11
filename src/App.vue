<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4 class="is-size-2">Pokedex</h4>
      <input type="text" class="input is-rounded" placeholder="Buscar Pokemon pelo nome" v-model="busca"/>
      <button class="button is-fullwidth is-success" id="botForm">Buscar</button>
      <div v-for="(poke, index) in resultadoBusca" :key="index">
     <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/APIPokemon.vue'

export default {
  name: 'App',
  data() {
    return{
      pokemons: [],
      busca: ''
    }
  },
    created: function() {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        console.log("Peguei lista pokemon")
        this.pokemons = res.data.results
      })
    },
    components: {
      Pokemon
    },
    computed: {
      resultadoBusca: function() {
    if (this.busca === '') {
      return this.pokemons;
    } else {
      return this.pokemons.filter(pokemon => 
        pokemon.name.toLowerCase().includes(this.busca.toLowerCase())
      );
    }
  }
    }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#botForm {
  margin-top: 2%;
}
</style>
