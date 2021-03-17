<template>
  <div id="app">
    
  </div>
</template>

<script>
import axios from 'axios'
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
