<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
       <dir v-for="(poke,index) in pokemons" :key="index">
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
      pokemons:[]
    }
  },
  created:function(){
    
    axios.get(url).then(res=>{
      
      this.pokemons = res.data.results
    })
  },
  components:{
    Pokemon
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
</style>
