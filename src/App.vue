<template>
  <div id="app">
    <main>
      <section>
          <div>
            <div
              v-for="pokemon in pokemons.slice(0, 50)" 
              :key="pokemon.name"
            >
              <div>
                <img 
                  :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${get_id(pokemon)}.svg`" 
                  :alt="pokemon.name"
                >
                <h2>{{get_name(pokemon)}}</h2>
              </div>
            </div>
          </div>
      </section>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',

  components: {},

  data: () => {
    return{
      pokemons: []
    }
  },

  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=100').then((response) => {
      this.pokemons = response.data.results;
    })
  },
  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split('/')[6])
    },
   get_name(pokemon) {
    return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
   } 
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
