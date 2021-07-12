<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light border-bottom">
    <div class="container">
      <a class="navbar-brand col-sm-3 col-md-2 mr-0 text-start" href="#"
        >Laravel Blog</a
      >

      <SearchInput @filters="onFilters"/>
    </div>
  </nav>
</template>

<script>
import SearchInput from "./SearchInput.vue";
export default {
  name: "Navbar",
  components: {
    SearchInput,
  },
  methods: {
    onFilters(datiInviatiDalEmit) {
      this.$emit("filters", datiInviatiDalEmit)
    }
  }
};
</script>