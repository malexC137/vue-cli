<template>
  <div id="app">
    <Navbar />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="container">
      <div class="row row-cols-3 g-4">
        <div class="col" v-for="index in 10" :key="index">
          <Card
            :title="'Titolo ' + index"
            :content="'Contenuto della <strong>card</strong> ' + index"
            linkText="Mostra dettagli"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Navbar from "./components/Navbar.vue";
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    // HelloWorld,
    Card,
    Navbar,
  },
};
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
