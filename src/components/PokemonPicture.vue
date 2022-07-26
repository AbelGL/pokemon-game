<template>
  <div class="pokemon-container">
    <img class="hidden-pokemon" :src="imgSrc" alt="Pokemon" />
    <img v-if="showPokemon" class="fade-in" :src="imgSrc" alt="Pokemon" />
  </div>
</template>

<script>
export default {
  name: "PokemonPicture",
  props: {
    pokemonId: {
      type: Number,
      required: true
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    }
  }
};
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
  height: 300px;
  margin-top: 30px;
  margin-bottom: 30px;
}
img {
  height: 300px;
  position: absolute;
  width: 100%;
  margin-left: -50vw;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
.hidden-pokemon {
  filter: brightness(0);
}
@media (max-width: 1023px) {
  .pokemon-container,
  .pokemon-container img {
    height: 260px;
  }
}
</style>