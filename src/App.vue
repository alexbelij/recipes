<template>
  <div id="app">
    <v-app>
      <recipes></recipes>
    </v-app>
  </div>
</template>

<script>
import Recipes from './components/Recipes';

export default {
  name: 'App',
  components: {
    Recipes,
  },
};
</script>

<style>
  body {
    height: 100vh;
    margin: 0;
    font-family: Verdana, sans-serif;
  }
  #app {
    width: 100%;
    height: 100%;
    background-color: #41B883;
    background: linear-gradient(to right, #41B883, #35495E);
  }
</style>
