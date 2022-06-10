<template>
  <div id="app" class="pt-5">
    <input
      class="input is-rounded mt-5 iinput"
      type="text"
      placeholder="Buscar Pokemón"
    />
    <button class="button botao is-info mt-1">Buscar</button>

    <div class="pokedex container">
      <div class="mb-5 mt-5" v-for="(poke, index) in pokemons" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";
export default {
  name: "App",
  components: {
    Pokemon,
  },
  data() {
    return {
      pokemons: [],
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
      });
  },
};
</script>

<style>
#app {
  background-color: #f5f6fa;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  /* padding: 0 250px; */
}
.pokedex {
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  justify-content: space-around;
}
.iinput,
.botao {
  width: 38% !important;
  display: block !important;
  margin: auto;
}

@media (max-width: 800px) {
  .iinput,
  .botao {
    width: 78 % !important;
    display: block !important;
    margin: auto;
  }
}
</style>
