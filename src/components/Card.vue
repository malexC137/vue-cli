<template>
  <div class="card text-start">
    <img :src="getImgUrl(img)" class="card-img-top" alt="" />

    <div class="card-body">
      <h5 :class="titleClass" class="card-title">{{ title }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">
        <span v-if="category">
          {{ category.name }}
        </span>

        <span v-if="tags">
          <span class="badge rounded-pill bg-primary" v-for="tag in tags" :key="tag.id">
            {{ tag.name }}
          </span>
        </span>
      </h6>

      <p class="card-text" v-html="getContent(content)"></p>

      <a href="#" @click="onLinkClick" class="card-link">{{ linkText }}</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    title: {
      type: String,
      required: true,
    },
    content: String,
    linkText: {
      type: String,
      default: "Mostra dettagli",
    },
    img: String,
    category: {
      type: Object,
      default: () => {
        return {};
      },
    },
    tags: Array,
    titleClass: String,
  },
  data() {
    return {
      variabile1: "",
    };
  },
  methods: {
    onLinkClick() {
      alert(this.title);
    },
    getImgUrl(url) {
      if (url) {
        return "http://127.0.0.1:8000/storage/" + url;
      }
      return "https://via.placeholder.com/350x150.png?text=Cover del post";
    },
    getContent(text) {
      const maxLength = 100;
      // aggiungere evidenziazione al testo cercato. Mark
      if (text.length > 100) {
        return text.slice(0, maxLength) + " ...";
      }
      return text;
    },
  },
};
</script>
Card