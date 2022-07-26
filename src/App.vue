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
  margin-top: 70px;
  max-width: 1200px;
}
html {
  background: url(http://localhost:8080/img/pokemon-background.d86d2d1c.png)
    no-repeat center bottom fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

@media (max-width: 1023px) {
  html {
    background: url(http://localhost:8080/img/pokemon-background.d86d2d1c.png)
      no-repeat 22% 50% fixed;
    background-size: cover;
  }
  h1 {
    font-size: 28px !important;
    line-height: 45px;
    padding: 0 15px;
    margin-bottom: 20px !important;
  }
}
</style>
