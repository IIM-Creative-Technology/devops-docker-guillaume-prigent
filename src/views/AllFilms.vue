<template>
  <div>
    <h1>FILMS</h1>
    <b-row class="justify-content-around">
      <div v-for="film in films" :key="film.imdbID">
        <b-col>
          <Card :film="film.imdbID"></Card>
        </b-col>
      </div>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";

import Card from "./../components/Card.vue";

export default {
  name: "AllFilms",
  components: {
    Card
  },
  props: {},
  data() {
    return {
      films: null
    };
  },
  mounted() {
    axios.get("https://www.omdbapi.com/?s=batman&apikey=f216d919").then(response => (this.films = response.data.Search));
  }
};
</script>

<style></style>
