<template>
  <div id="pokemon">
    
    <small>{{ url }}</small>

    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="pokemon.front"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          
          </div>
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
          
        </div>
      </div>
    </div>

  </div>
</template>
<script>
import axios from "axios";

export default {
  created: async function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      console.log(this.pokemon);
    });
  },
  data() {
    return {
      pokemon: {
          type:"",
          front:"",
          back:""
      },
    };
  },
  props: {
    name: String,
    url: String,
    num: Number,
  },
  filters: {
    upper: function (value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
};
</script>

<style scoped>
#pokemon{
    margin-top:2%;

}
</style>