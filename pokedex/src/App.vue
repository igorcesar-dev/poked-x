<template>
  <div id="app">
    <img class="mb-5" src="./assets/pokemonlogo.png" alt="logo" />
    <br />
    <input
      class="mb-3 rounded w-50"
      type="text"
      placeholder="Buscar pokémon pelo nome"
      v-model="busca"
    /><br />
    <button
      @click="buscar"
      class="mb-5 rounded w-50 btn-primary btn"
      id="buscaBtn"
    >
      Buscar
    </button>
    <br />
    <button @click="mostrarTodos">Exibir todos os Pokémos</button>
    <div class="container">
      <div class="row">
        <div
          class="col-sm"
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
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons;
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

.modal-content{
  background-color: unset;
}
</style>
