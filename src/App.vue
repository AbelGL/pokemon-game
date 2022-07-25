<template>
  <div>
    <PokemonPage />
  </div>
</template>

<script>
import PokemonPage from "@/pages/PokemonPage";

export default {
  name: "App",
  components: {
    PokemonPage
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 150px;
  max-width: 1200px;
}
html {
  background: url(../src/assets/pokemon-background.png)
    no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}
</style>
