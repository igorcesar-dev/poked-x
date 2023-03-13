<template>
  <div id="app">
    <img class="mb-4" src="./assets/pokemonlogo.png" alt="logo" />
    <br />
    <input
      class="mb-3 rounded-3 w-50 text-center" style="border:solid 0.1px"
      type="text"
      placeholder="Buscar pokémon pelo nome"
      v-model="busca"
    /><br />
    <button class="button-app mb-4"
      @click="buscar"
      id="buscaBtn"
    >
      Buscar
    </button>
    <div class="container">
      <div class="row">
        <div
          class="col-sm mb-3 text-center"
          v-for="(poke, index) in filteredPokemons"
          :key="poke.url"
        >
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/PokemonView.vue";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("pegou a lista de pokemons");
        this.pokemons = res.data.results;
        this.filteredPokemons = this.pokemons;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca
        );
      }
    },
  },

  computed: {
    resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  background: linear-gradient(to bottom, #6ab7f5, #fff);
}

.button-app {
  width: 30%;
  border: 2px solid #000;
  border-radius: 5px;
  font-size: clamp(8px, 5vw, 1rem);
  font-weight: 600;
  color: white;
  background-color: #444;
  box-shadow: -2px 3px 0 #222, -4px 6px 0 #000;
}
.button-app:active {
  box-shadow: inset -4px 4px 0 #222;
  font-size: 0.9rem;
}
</style>
