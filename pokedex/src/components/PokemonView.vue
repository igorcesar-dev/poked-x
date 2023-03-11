<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <div class="card" style="width: 20rem">
          <img :src="currentImg" class="card-img-top" alt="img" />
          <div class="card-body">
            <h5 class="card-title">{{ num }} - {{ upper(name) }}</h5>
            <p class="card-text">Tipo: {{ pokemon.type }}</p>
            <button
              type="button"
              class="btn btn-primary"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
            >
              Exibir detalhes
            </button>

            <div
              class="modal fade"
              id="exampleModal"
              tabindex="-1"
              aria-labelledby="exampleModalLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog w-25">
                <div class="modal-content" style="background-color: unset;border: none">
                  <img @click="mudarSprite" :src="currentImg" alt="pokemon" class="pokemon_image" />

                  <h1 class="pokemon__data">
                    <span class="pokemon__number">{{ num }}</span> -
                    <span class="pokemon__name">{{ upper(name) }}</span>
                  </h1>

                  <div class="buttons">
                    <button
                      type="button"
                      class="btn btn-secondary button btn-prev"
                      data-bs-dismiss="modal"
                    >
                      Sair &lt;
                    </button>
                  </div>

                  <img
                    src="../assets/pokedex.png"
                    alt="pokedex"
                    class="pokedex"
                  />
               
                </div>
              </div>
            </div>
          </div>
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
      console.log(res);
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

@import url("https://fonts.googleapis.com/css2?family=Oxanium:wght@300;400;500;600;700;800&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Oxanium", cursive;
}

body {
  text-align: center;
  background: linear-gradient(to bottom, #6ab7f5, #fff);
  min-height: 100vh;
}

main {
  display: inline-block;
  margin-top: 2%;
  padding: 15px;
  position: relative;
}

.pokedex {
  width: 100%;
  max-width: 425px;
}

.pokemon_image {
  position: absolute;
  width: 30%;
  bottom: 55%;
  left: 50%;
  transform: translate(-63%, 20%);
  
}

.pokemon__data {
  position: absolute;
  font-weight: 600;
  color: #aaa;
  top: 54.5%;
  right: 27%;
  font-size: clamp(8px, 5vw, 25px);
}

.pokemon__name {
  color: #3a444d;
  text-transform: capitalize;
}

.form {
  position: absolute;
  width: 65%;
  top: 65%;
  left: 13.5%;
}

.input__search {
  width: 100%;
  padding: 4%;
  outline: none;
  border: 2px solid #333;
  border-radius: 5px;
  font-weight: 600;
  color: #3a444d;
  font-size: clamp(8px, 5vw, 1rem);
  box-shadow: -3px 4px 0 #888, -5px 7px 0 #333;
}

.buttons {
  position: absolute;
  bottom: 10%;
  left: 50%;
  width: 65%;
  transform: translate(-57%, 0);
  display: flex;
  gap: 20px;
}

.button {
  width: 50%;
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

.bk-black{
  background-color: #000;
}

.modal-bk{
  background-color: transparent;
}
</style>