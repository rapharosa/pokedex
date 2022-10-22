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
        <section class="info">
          <img :src="pokemon?.sprites.other.dream_world.front_default || pokemon?.sprites.front_default " :alt="pokemon?.name">
          <div>
            <p v-for="stat in pokemon?.stats" :key="stat.slot"> {{ stat.stat.name }}: {{ stat.base_stat }}</p>
          </div>
        </section>

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