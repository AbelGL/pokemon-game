<template>
  <div>
    <h1 v-if="!pokemon">Espere porfavor...</h1>
    <div v-else>
      <h1>¿Quién es este pokémon?</h1>
      <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
      <PokemonOptions v-if="!optionsClicked" :pokemons="pokemonArr" @selection="checkAnswer" />
      <template v-if="showAnswer" class="fade-in">
        <h2>{{message}}</h2>
        <div class="pokemonCounter" v-if="enableCounter">
          <div>
            <span v-if="hitsCount > 0" class="hits-span">
              <b>{{hitsCount}}</b><span>Aciertos</span>
            </span>
            <span v-if="failsCount > 0" class="fails-span">
              <b>{{failsCount}}</b><span>Fallos</span>
            </span>
          </div>
        </div>
        <button class="reset-button" @click="resetGame">Siguiente</button>
      </template>
    </div>
  </div>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture";
import PokemonOptions from "@/components/PokemonOptions";
import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  name: "PokemonPage",
  components: {
    PokemonPicture,
    PokemonOptions
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
      hitsCount: 0,
      failsCount: 0,
      optionsClicked: false,
      enableCounter: false
    };
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions();
      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(pokemonId) {
      this.showPokemon = true;
      this.showAnswer = true;
      this.optionsClicked = true;
      this.enableCounter = true;
      if (pokemonId === this.pokemon.id) {
        this.message = `Correcto, ${this.pokemon.name}`;
        this.hitsCount += 1;
      } else {
        this.message = `Oops, era ${this.pokemon.name}`;
        this.failsCount += 1;
      }
    },
    resetGame() {
      this.enableCounter = true;
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.optionsClicked = false;
      this.mixPokemonArray();
    }
  },
  mounted() {
    this.mixPokemonArray();
  }
};
</script>

<style scoped>
.reset-button {
  color: #fff;
  background-color: #42b883;
  border: 0;
  padding: 1em 2.8em;
  font-family: "Montserrat", sans-serif;
  border-radius: 5px;
  margin-bottom: 50px;
  margin-top: 30px;
  cursor: pointer;
}

.hits-span b {
  color: #199b19;
}

.fails-span b {
  color: red;
}

.happyFace img,
.sadFace img {
  width: 100px;
}

.pokemonCounter {
  padding: 20px;
  border-radius: 40px;
}

.pokemonCounter > div {
  border-radius: 22px;
  padding: 20px px;
  width: auto;
  text-align: center;
  gap: 20px;
  margin: 0 auto;
}

.pokemonCounter span {
  font-size: 25px;
  padding: 10px;
}

.pokemonCounter span b {
  font-size: 50px;
  margin-right: 4px;
}
</style>
