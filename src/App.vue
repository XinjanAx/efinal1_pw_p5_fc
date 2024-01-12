<template>
  <poke-juego />
</template>

<script>
import PokeJuego from './components/PokeJuego.vue'

export default {
  name: 'App',
  components: {
    PokeJuego
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
