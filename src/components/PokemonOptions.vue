<template>
  <div class="options-container">
    <ul>
      <li
        class="option-item"
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id)"
      >
        <span>{{pokemon.name}}</span>
      </li>
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
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
}

.options-container {
  display: flex;
  justify-content: center;
}

.option-item {
  box-sizing: border-box;
  cursor: pointer;
  align-self: center;
  font-size: 1rem;
  line-height: 1;
  margin: 10px;
  padding: 0px 20px;
  text-decoration: none;
  text-align: center;
  border: 3px solid #50514f;
  text-transform: uppercase;
  display: inline;
  position: relative;
  border-radius: 5px;
}

.option-item::before {
  position: absolute;
  content: "";
  top: 0;
  left: 0;
  width: 100%;
  height: 50%;
  transform: translate3d(0, 0, 0);
  transition: transform 0.25s;
  transition-timing-function: cubic-bezier(0.2, 1, 0.3, 1);
}

.option-item::after {
  top: 50%;
  background: #fff;
}

.option-item {
  transition: box-shadow 300ms ease-in-out, color 300ms ease-in-out;
}

.option-item span {
  font-size: 1rem;
  transition: color 0.5s 0.25s;
  display: inline-block;
  position: relative;
  z-index: 999;
}

.option-item:hover {
  top: -10px;
  transition: top ease 0.5s;
}
@media (max-width: 1023px) {
  ul {
    margin-top: 20px;
  }
  .option-item {
    display: inline-block;
    margin: 7px;
    padding: 15px;
    font-size: 0.6rem;
  }
  .option-item span {
    font-size: 0.7rem;
  }
}
</style>