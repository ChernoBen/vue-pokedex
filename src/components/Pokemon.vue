<template>
  <div id="poke">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="pokemon.front" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media"></div>
        <div class="media-content">
          <p class="title is-4">{{ num }} - {{ name | upper }}</p>
          <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
      </div>

      <div class="content">
        <button class="button is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  created: async function () {
    await axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
      console.log(this.pokemon);
    });
  },
  data() {
    return {
      currentImg: "",
      isFront: true,
      pokemon: {
        type: "",
        front: "",
        back: "",
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
  methods: {
    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      }else{
          this.isFront = true
          this.currentImg = this.pokemon.front
      }
    },
  },
};
</script>

<style scoped>
#poke {
  margin-top: 2%;
}
</style>