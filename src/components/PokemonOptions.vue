<template>
  <div class="options-container">
    <ul>
      <li
        class="option-item"
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >{{pokemon.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PokemonOptions",
  props: {
    pokemons: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
/* Pokemon Options */
ul {
  list-style-type: none;
  padding: 0;
  margin-top: 50px;
}
li {
  background-color: white;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
  display: flex;
  justify-content: center;
}

.option-item {
  box-sizing: border-box;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border: 2px solid #35495e;
  border-radius: 21px;
  cursor: pointer;
  align-self: center;
  font-size: 1rem;
  line-height: 1;
  margin: 20px;
  padding: 0px 20px;
  text-decoration: none;
  text-align: center;
  text-transform: uppercase;
  background-color: #000000b3;
  display: inline;
  color: #fff;
}

.option-item {
  transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
}

.option-item:hover,
.option-item:focus {
  color: #fff;
  outline: 0;
}

.option-item:hover {
  box-shadow: 0 0 40px 40px #35495e inset;
}
</style>