<template>
  <b-card :title="filmData.Title" :img-src="filmData.Poster" :img-alt="filmData.Title" img-top tag="article" style="max-width: 20rem;" class="mb-3">
    <b-card-text> {{ filmData.Plot }}, <br /> </b-card-text>
    <b-card-text> Année de sortie : {{ filmData.Year }} </b-card-text>

    <div class="bottomLinks">
      <b-button :href="`#/details/${film}`" variant="primary mr-2">Plus d'infos !</b-button>
      <b-button href="#" variant="primary" v-on:click="newFav(film)">Favori</b-button>
    </div>
  </b-card>
</template>

<script>
import axios from "axios";
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

export default {
  name: "Card",
  props: {
    film: String
  },
  data() {
    return {
      filmData: {}
    };
  },
  state: {
    favorites: ""
  },
  methods: {
    newFav(item) {
      this.$store.commit("newFav", item);
    }
  },
  mounted() {
    axios.get("https://www.omdbapi.com/?i=" + this.film + "&apikey=f216d919").then(response => (this.filmData = response.data));
  }
};
</script>

<style scoped>
.card-text {
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}
img {
  width: 100%;
  height: 20vw;
  object-fit: cover;
}
</style>
