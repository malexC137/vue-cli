<template>
  <div id="app">
    <Navbar @filters="onFilters" />

    <main class="container py-5">
      <TextInput label="Input di prova" v-model="textInputValue" />

      <TextAreaInput label="Input di prova" v-model="textInputValue" />
      <!-- :value="textInputValue"
                  @input="textInputValue = $event" -->

      <div class="alert alert-success" v-if="datiFiltro">
        Sono stati trovati {{ postsList.length }} risulati per il filtro:
        <div v-html="printActiveFilters()"></div>

        <a href="#" class="btn btn-link" @click="resetFilter">Annulla filtri</a>
      </div>

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
    </main>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Navbar from "./components/Navbar.vue";
import TextInput from "./components/TextInput.vue";
import TextAreaInput from "./components/TextAreaInput.vue";
//import HelloWorld from './components/HelloWorld.vue'
export default {
  name: "App",
  components: {
    //HelloWorld,
    Card,
    Navbar,
    TextInput,
    TextAreaInput,
  },
  data() {
    return {
      title: "La mia prima pagina con vue cli",
      postsList: [],
      allPosts: [],
      datiFiltro: null,
      countFiltro: 0,
      textInputValue: "",
    };
  },
  computed: {},
  methods: {
    onFilters(datiRicevuti) {
      const searchedContent = datiRicevuti.filters.content;
      this.postsList = datiRicevuti.results.map((post) => {
        const esprReg = new RegExp(searchedContent, "g");
        post.content = post.content.replace(
          esprReg,
          `<span class="marked">${searchedContent}</span>`
        );
        return post;
      });
      this.datiFiltro = datiRicevuti.filters;
      this.countFiltro = datiRicevuti.results.length;
    },
    printActiveFilters() {
      const toReturn = [];
      if (Object.keys(this.datiFiltro).length === 0) {
        return;
      }
      for (const chiaveFiltro in this.datiFiltro) {
        toReturn.push(chiaveFiltro + " = " + this.datiFiltro[chiaveFiltro]);
      }
      return toReturn.join("<br>");
    },
    resetFilter() {
      this.postsList = this.allPosts;
      this.datiFiltro = null;
      this.countFiltro = 0;
    },
  },
  mounted() {
    this.axios
      .get("http://127.0.0.1:8000/api/posts")
      .then((resp) => {
        this.allPosts = resp.data.results;
        this.postsList = resp.data.results;
      })
      .catch((er) => {
        console.error(er);
        alert("Errore nel caricamento dei dati.");
      });
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
.marked {
  background-color: yellow;
}
</style>

Card