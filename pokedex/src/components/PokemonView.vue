<template>
  <div>
    <div class="card" style="width: 20rem">
      <img :src="currentImg" class="card-img-top" alt="img" />
      <div class="card-body">
        <h5 class="card-title">{{ num }} - {{ upper(name) }}</h5>
        <p class="card-text">
          {{ pokemon.type }}
        </p>
        <button @click="mudarSprite" class="btn btn-primary">
          Mudar sprite
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  methods: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
  },
};
</script>

<style>
.card {
  margin: 0 auto; /* Added */
  float: none; /* Added */
  margin-bottom: 10px; /* Added */
}
</style>