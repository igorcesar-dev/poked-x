# Pokedéx com Vue.JS           

Este projeto foi criado durante a realização do curso de Formação Node.JS na Udemy com o professor Victor Lima. Foi utilizada a API <a href="https://pokeapi.co/">PokéAPI</a> para obter os dados.

## Technologies 💻
* Vue
* Bootstrap
* Axios

## Installation ⚙️

* Vue.JS
```bash
npm install -g @vue/cli
```

* Axios
```bash
npm install axios
```

## Import ⤵️

```bash
import "../node_modules/bootstrap/dist/css/bootstrap.css"
import "../node_modules/bootstrap/dist/js/bootstrap.js"
```

## API 🔄
```bash
created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = this.pokemons;
      });
  },
```
## Run project 🏃
```bash
npm run serve
```

## Result 🌐
<img src="/src/assets/poke.gif" />
