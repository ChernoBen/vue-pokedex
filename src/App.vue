<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokemon.png" >
      <hr>
      <h4 class="is size-7">Pokedex</h4><br>
      <input class="input is-rounded" type="text" placeholder="Buscar Pokemon" v-model="busca">
      <button class="button is-medium is-halfwidth is-success" id="buscaBtn" @click="buscarPoke">Buscar</button>  
       <dir v-for="(poke,index) in filteredPokemons" :key="poke.url">
      <Pokemon :name="poke.name" :url="poke.url" :num="index"/>
    </dir>
    </div>
   
    
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

let url = "https://pokeapi.co/api/v2/pokemon?limit=151&offset=0"

export default {
  name: 'App',
  data(){
    return {
      pokemons:[],
      filteredPokemons:[],
      busca:""
    }
  },
  created:function(){
    
    axios.get(url).then(res=>{
      
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  components:{
    Pokemon
  },
  methods:{

    buscarPoke:function(){

      this.filteredPokemons = this.pokemons
      if(this.busca =="" || this.busca == " "){

        this.filteredPokemons =  this.pokemons

      }else {

        this.filteredPokemons =  this.pokemons.filter(pokemons=>pokemons.name == this.busca)
      }

    }
  },
  computed:{
    // resultado:function(){
    //   if(this.busca =="" || this.busca == " "){
    //     return this.pokemons
    //   }else {
    //     return this.pokemons.filter(pokemons=>pokemons.name == this.busca)
    //   }
    // }
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
#buscaBtn{
  margin-top:2%;
}
</style>
