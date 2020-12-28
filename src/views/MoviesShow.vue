<template>
  <div class="movies-show">
    <h1>Movie Details</h1>

   
      <img :src="movie.image">
      <h1>{{ this.movie.title }}</h1>
      <p>{{ movie.release_year }}</p>
      <p>{{ movie.description }}</p>
      <p>Thumbs up: {{ movie.thumbs_up }}</p>
      <p>Thumbs down: {{ movie.thumbs_down }}</p>
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
      movie: {},
    };
  },
  created: function () {
    this.moviesShow();
  },
  methods: {
    moviesShow: function () {
      axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
        this.movie = response.data;
        console.log(this.movie);
      });
    },
  },
};
</script>
