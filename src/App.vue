<template>
  <div id="app">

    <CabecalhoPokedex titulo='Pokedex'/>
    
    <main>

      <section class="busca">
        <label for="pesquisa">Pokemon:</label>
        <input name="pesquisa" v-model="search" placeholder="Busque um Pokemon" />
      </section>

      <section class="sessao-lista">
        <div
          v-for="pokemon in filtered_pokemons" 
          :key="pokemon.name"
          
        >
          <div @click="show_pokemon(pokemon.name)" class="lista">
            <h3>{{get_name(pokemon)}}</h3>
            <img 
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png`" 
              :alt="pokemon.name"
            >
          </div>

        </div>
      </section>
        <ModalPokemon :pokemon="selected_pokemon" :closeModal="onCloseModal" :visible="!!selected_pokemon"/>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import ModalPokemon from './components/ModalPokemon/ModalPokemon.vue';
import CabecalhoPokedex from './components/Cabecalho/CabecalhoPokedex.vue';

export default {
  name: 'App',

  components: {
    ModalPokemon,
    CabecalhoPokedex
},

  data: () => {
    return{
      pokemons: [],
      search: '',
      selected_pokemon: null,
    }
  },

  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=10000').then((response) => {
      this.pokemons = response.data.results;
    })
  },

  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split('/')[6])
    },

   get_name(pokemon) {
    return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
   },

   show_pokemon(id) {
    axios
    .get(`https://pokeapi.co/api/v2/pokemon/${id}`)
    .then((response) => {
      this.selected_pokemon = response.data
    });
   },

   onCloseModal(){
    this.selected_pokemon = null;
   },

  },

  computed: {
    filtered_pokemons(){
      if(!this.search){
        return []
      }
      return this.pokemons.filter((item) => {
          return item.name.includes(this.search.toLowerCase())
      }).slice(0, 20);
    },

    selected_pokemon_name(){
      if (this.selected_pokemon){
        return this.selected_pokemon.name
      } return 'Carregando';
    }
  }
}

</script>

<style src="./style.css"/>