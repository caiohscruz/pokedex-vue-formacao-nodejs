<template>
  <div id="app">
    <div class="navbar">
      <div class="nav-item">
        <img :src="logo" id="logo">
      </div>
      <div class="nav-item">
        <input type="text" placeholder="Search by the name" class="input" v-model="searchName">
        <button class="button is-info" @click="Search()">Search</button>
      </div>
      <div class="nav-item">
        <div id="types">
          <div v-for="type in types" :key="type">
            <button @click="FilterType(type)">{{type}}</button>
          </div>
        </div>
      </div>
    </div>
    <hr>
    <div id="pokemon-list">
      <div v-for="poke in filteredPokemons" :key='poke.url'>
          <PokemonCard :name="poke.name" :url="poke.url" @addType="AddType" />
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import PokemonCard from "./components/PokemonCard.vue";

  export default {
    name: 'App',
    data() {
      return {
        pokemons: [],
        filteredPokemons: [],
        searchName: "",
        searchType: "",
        types: []
      }
    },
    created: function () {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        res.data.results.forEach(pokemon => {
          this.pokemons.push({
            name: pokemon.name,
            url: pokemon.url,
            types: []
          })
        })
        this.filteredPokemons = this.pokemons;
        this.types.push("all");
      })
    },
    components: {
      PokemonCard,

    },
    computed: {
      logo() {
        return require("./assets/pokemon_logo.png")
      },
    },
    methods: {
      Search() {
        if (this.searchName.trim() == "" || this.searchName.trim() == " ") {
          this.filteredPokemons = this.pokemons;
        } else {
          var regex = new RegExp(this.searchName.toUpperCase());
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toUpperCase().match(regex));
        }
      },
      AddType(item) {
        if (!this.types.includes(item.name)) {
          this.types.push(item.name);
          this.types.sort();
        }
        this.pokemons[item.pokemonId - 1].types.push(item.name);
      },
      FilterType(type) {
        if (type == "all") {
          this.filteredPokemons = this.pokemons;
        } else {
          this.filteredPokemons = null;
          this.pokemons.forEach(pokemon => {
            if(pokemon.types.includes(type)){
              this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.types.includes(type));
            }
          })
        }
      },
    }
  }
</script>

<style>
  .navbar {
    display: flex;
    flex-flow: wrap;
    justify-content: space-evenly;
  }

  .nav-item {
    display: flex;
    align-items: center;
    margin: 1%;
  }

  .nav-item>#types {
    display: flex;
    flex-flow: wrap;
  }

  #types>div {
    display: flex;
  }

  #logo {
    margin-left: 1%;
    margin-right: 1%;
    margin-top: 1%;
    width: 200px;
    height: 73.6px;
  }

  #pokemon-list {
    display: flex;
    flex-flow: wrap;
    justify-content: center;
    align-content: center;
  }

  #pokemon-list>div {
    margin: 1%;
  }
</style>