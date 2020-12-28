<template>
  <div class="home">
    <h1>Movie Rater</h1>

    <div v-for="movie in movies">
      <img :src="movie.image">
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.release_year }}</p>
      <p>{{ movie.description }}</p>
      <p>Thumbs up: {{ movie.thumbs_up }}</p>
      <p>Thumbs down: {{ movie.thumbs_down }}</p>
    </div>
  </div>
</template>

<style>
img {
  max-height: 250px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: {},
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      axios.get("api/movies").then((response) => {
        this.movies = response.data;
        console.log(this.movies);
      });
    },
  },
};
</script>
