<template>
  <div class="modal">
    <section name="fade" >
      <div class="teste-fade" v-if="!!visible"></div>
    </section>

    <section>
      <div class="card" v-if="visible">
        <section>
          <h1>{{pokemon?.name.charAt(0).toUpperCase() + pokemon.name.slice(1)}}</h1>
        </section>
        <img :src="pokemon?.sprites.other.dream_world.front_default || pokemon?.sprites.front_default" :alt="pokemon?.name">
        <button @click="closeModal()">Fechar</button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'ModalPokemon',
  props: {
    pokemon: Object,
    visible: Boolean,
    closeModal: Function
  }
}
</script>

<style src="./style.css" scoped />