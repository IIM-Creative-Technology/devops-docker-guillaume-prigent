<template>
  <div>
    <b-row class="pt-2">
      <b-col cols="5">
        <b-img :src="filmData.Poster" fluid :alt="filmData.Title"></b-img>
      </b-col>
      <b-col cols="7">
        <h1 class="pb-3">{{ filmData.Title }}, {{ filmData.Year }}</h1>
        <b-row>
          <b-col cols="6">
            <h5>Note : {{ filmData.Ratings[0].Value }}</h5>
            <h5>Genres : {{ filmData.Genre }}</h5>
          </b-col>
          <b-col cols="6">
            <h5>Durée : {{ filmData.Runtime }}</h5>
            <h5>PEGI : {{ filmData.Rated }}</h5>
          </b-col>
          <b-col cols="12" class="mt-4">
            <p>{{ filmData.Plot }}</p>
          </b-col>
        </b-row>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Details",
  components: {},
  props: {},
  data() {
    return {
      filmData: null
    };
  },
  mounted() {
    axios.get("https://www.omdbapi.com/?i=" + this.$route.params.id + "&apikey=f216d919").then(response => (this.filmData = response.data));
  }
};
</script>

<style scoped></style>
