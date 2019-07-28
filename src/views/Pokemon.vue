<template>
  <div>
    <router-link to="/"><h1>Home</h1></router-link>
    <span v-if="loading">
      <h1>Loading...</h1>
    </span>
    <card
      class="column is-2 has-text-centered"
      :pokemon="pokemon"
      v-else-if="pokemon"
    />
  </div>
</template>

<script>
import Card from "../components/Card";
import { computed, onMounted } from "vue-function-api";

export default {
  name: "pokemon",
  components: { Card },
  props: {
    id: String
  },
  setup(props, context) {
    const pokemon = computed(() => {
      return context.root.$store.getters.pokemonDetail[props.id];
    });

    const loading = computed(() => {
      return context.root.$store.getters.loading;
    });

    onMounted(() => {
      context.root.$store.dispatch("LOAD_POKEMON_DETAIL", {
        pokemonId: props.id
      });
    });

    return {
      pokemon,
      loading
    };
  }
};
</script>

<style scoped></style>
