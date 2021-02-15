<template>
  <div id="app">  
    <div class="column is-half is-offset-one-quarter">
       <input class="input is-rounded" type="text" placeholder="Buscar pokemon" v-model="poke.url"> 
      <button id="btn-busca" class="button is-rounded is-info" @click="buscar">Buscar</button>
      <div v-for = "(poke, index) in filterPokemons" :key= "index">
      <pokemon :name="poke.name" :url="poke.url" :num = "index + 1" />
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  data(){
    return{
      pokemons: [],
      filterPokemons: [],
       busca: ''
    }
  },
 created: function(){
   console.log("teste");
   axios.get("https://pokeapi.co/api/v2/pokemon?limit=100&offset=200").then( res => {
      this.pokemons = res.data.results;
      this.filterPokemons = res.data.results;
   })
 },
  components: {
   Pokemon
 },

 methods:{
   buscar: function(){
     this.filterPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
       this.filterPokemons = this.pokemons
     }else{
       this.filterPokemons = this.pokemons.filter(Pokemon => Pokemon.name == this.busca);
     }

   }
 }
}
</script>

<style>
#btn-busca{
  margin-top: 5px;
}
</style>
