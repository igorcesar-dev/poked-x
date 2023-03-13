<template>
  <div>
    <div class="card text-center rounded-4" style="width: 15rem">
      <img :src="currentImg" class="card-img-top" alt="img" />
      <div class="card-body">
        <h1 class="pokemon__data">
          <span class="pokemon__number">{{ num }}</span> -
          <span class="pokemon__name">{{ upper(name) }}</span>
        </h1>
        <p class="card-text pokemon__name">Tipo: {{ pokemon.type }}</p>
        <div class="buttons">
          <button
            type="button"
            class="btn btn-secondary button btn-prev"
            data-bs-dismiss="modal"
            @click="mudarSprite"
          >
            Mudar sprite &lt;
          </button>
        </div>
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
      this.namePoke = this.pokemon.type;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        name: "",
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
.pokemon__data {
  font-weight: 600;
  color: #aaa;
  font-size: clamp(8px, 5vw, 25px);
}
.button {
  padding: 4%;
  border: 2px solid #000;
  border-radius: 5px;
  font-size: clamp(8px, 5vw, 1rem);
  font-weight: 600;
  color: white;
  background-color: #444;
  box-shadow: -2px 3px 0 #222, -4px 6px 0 #000;
}
.button:active {
  box-shadow: inset -4px 4px 0 #222;
  font-size: 0.9rem;
}
</style>