<template>
  <!-- Result set -->
  <div class="resultset">
    <div class="columns is-multiline">
      <div v-if="loading">
        <h1>Loading...</h1>
      </div>

      <router-link
        class="column is-2 has-text-centered"
        v-for="pokemon of filteredPokemons"
        :to="`/pokemon/${pokemon.id}`"
        :key="pokemon.id"
      >
        <!-- Pokemon -->
        <card :pokemon="pokemon" v-if="!loading"></card>
      </router-link>
    </div>
  </div>
</template>

<script>
import Card from "./Card";
import { computed, onMounted } from "vue-function-api";

export default {
  name: "result",
  components: {
    Card
  },
  props: {
    criteria: String
  },
  setup(props, context) {
    const pokemons = computed(() => {
      return context.root.$store.getters.pokemons;
    });

    const filterOnPokemon = pokemon => {
      const lowerSearch = props.criteria.toLowerCase();
      const lowerPokemon = pokemon.name.toLowerCase();
      return lowerPokemon.includes(lowerSearch);
    };

    const filteredPokemons = computed(() => {
      return pokemons.value.filter(pokemon => filterOnPokemon(pokemon));
    });

    const loading = computed(() => {
      return context.root.$store.getters.loading;
    });

    onMounted(() => {
      context.root.$store.dispatch("LOAD_POKEMONS");
    });

    return {
      pokemons,
      filteredPokemons,
      loading,
      filterOnPokemon
    };
  }
};
</script>

<style scoped></style>
