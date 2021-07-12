<template>
  <div id="app">
    <Navbar />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="container">
      <div class="row row-cols-3 g-4">
        <div class="col" v-for="post in postsList" :key="post.id">
          <Card
            :title="post.title"
            :content="post.content"
            :img="post.cover_url"
            :category="post.category"
            :tags="post.tags"
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
  data() {
    return {
      title: "La mia prima pagina con Vue Cli",
      postsList: [],
    };
  },
  computed: {},
  methods: {},
  mounted() {
    this.axios.get("http://127.0.0.1:8000/api/posts")
    .then(resp => {
      this.postsList = resp.data.results;
    })
    .catch((er) => {
      console.error(er);
      alert("Errore nel caricamento dati.")
    })
  }
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
