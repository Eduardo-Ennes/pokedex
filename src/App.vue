<template>
  <div class="app">
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded inp" type="text" placeholder="Buscar pokemon" v-model="busca">
      <button class="button is-fullwidth but" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon'
import axios from 'axios'
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    }).catch(() => {
      
    })
  }, 
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        return this.filteredPokemons = this.pokemons
      }
      else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {
    // resultadoBusca: function(){
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons
    //   }
    //   else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }
    // }
  }
}
</script>

<style>
 .app{
  padding: 1rem 0 1rem 2rem;
 }

 .but{
  margin: 1rem 0;
 }
</style>
