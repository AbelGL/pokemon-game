<template>
  <div>
    <div v-if="areYouDead" class="dead-game-container">
      <h1>Lo siento has muerto!</h1>
      <img src="../assets/dead.gif" alt="Dead" />
      <button class="reset-button end-game" @click="resetGame">Reiniciar juego</button>
    </div>
    <div v-else>
      <div class="end-game-container" v-if="endGame">
        <h1>Enhorabuena has ganado el juego!</h1>
        <img src="../assets/happy.gif" alt="Happy" />
        <button class="reset-button end-game" @click="resetGame">Reiniciar juego</button>
      </div>
      <div class="pokemon-game-container" v-else>
        <h1 v-if="!pokemon">Espere porfavor...</h1>
        <div v-else>
          <div v-if="!endGame">
            <h1>¿QUIÉN ES ESTE POKÉMON?</h1>
            <p>Tienes 3 intentos, si fallas 3 veces, fin del juego. Si llegas a 50 aciertos ganas!</p>
            <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
            <PokemonOptions v-if="!optionsClicked" :pokemons="pokemonArr" @selection="checkAnswer" />
          </div>
          <template v-if="!endGame" class="fade-in">
            <h2 v-if="showAnswer">{{message}}</h2>
            <div class="pokemonCounter" v-if="enableCounter">
              <div>
                <span v-if="hitsCount > 0" class="hits-span">
                  <b>{{hitsCount}}</b>
                  <span>Aciertos</span>
                </span>
                <span v-if="failsCount > 0" class="fails-span">
                  <b>{{failsCount}}</b>
                  <span>Fallos</span>
                </span>
              </div>
            </div>
            <button
              v-if="!endGame && optionsClicked"
              class="reset-button"
              @click="nextGame"
            >Siguiente</button>
          </template>
        </div>
      </div>
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
      endGame: false,
      areYouDead: false,
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
      hitsCount: 0,
      failsCount: 0,
      optionsClicked: false,
      enableCounter: false,
      LIMIT: 50
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
      if (this.hitsCount === this.LIMIT) {
        this.endGame = true;
      }
      if (this.failsCount === 3) {
        this.areYouDead = true;
      }
    },
    nextGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.optionsClicked = false;
      this.enableCounter = true;
      this.mixPokemonArray();
    },
    resetGame() {
      this.enableCounter = true;
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonArr = [];
      this.pokemon = null;
      this.optionsClicked = false;
      this.hitsCount = 0;
      this.failsCount = 0;
      this.endGame = false;
      this.areYouDead = false;
      this.mixPokemonArray();
    }
  },
  mounted() {
    this.mixPokemonArray();
  }
};
</script>

<style scoped>
.pokemon-game-container h1,
.dead-game-container h1,
.end-game-container h1,
h2 {
  text-shadow: -1px 1px 3px #2c3e50;
}
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

.pokemon-game-container p {
  max-width: 488px;
  margin: 0 auto;
  font-size: 13px;
  line-height: 20px;
  margin-bottom: 20px;
}

.dead-game-container,
.end-game-container {
  margin-top: 100px;
  overflow: hidden;
}

.dead-game-container img,
.end-game-container img {
  border-radius: 50%;
  height: 400px;
  width: 450px;
}

.dead-game-container .reset-button,
.end-game-container .reset-button {
  margin: 10px auto;
  display: block;
  margin-top: 30px;
}

.end-game {
  background-color: #ef594f;
}

.hits-span b {
  color: #199b19;
}

.fails-span b {
  color: #ef594f;
}

.happyFace img,
.sadFace img {
  width: 100px;
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

@media (max-width: 1023px) {
  .pokemon-game-container p {
    max-width: initial;
    padding: 0 15px;
  }
  .dead-game-container img,
  .end-game-container img {
    height: 310px;
    width: 92%;
  }
  .pokemonCounter span {
    font-size: 18px;
    padding: 10px;
    line-height: 25px;
  }
  .pokemonCounter span b {
    font-size: 28px;
  }
}
</style>
