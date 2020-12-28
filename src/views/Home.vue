<template>
  <div class="home">

    <div v-for="movie in movies">
      <router-link v-bind:to="`/movies/${movie.imdb_id}`">
        <img :src="movie.image">
      </router-link>
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.release_year }}</p>
      <p>{{ movie.description }}</p>
      <!-- <p>Thumbs Up: {{ movie.thumbs_up }}</p>
      <p>Thumbs Up: {{ movie.thumbs_down }}</p> -->
      <p><button v-on:click="thumbsUp(movie)">Thumbs Up</button>: {{ movie.thumbs_up }}</p>
      <p><button v-on:click="thumbsDown(movie)">Thumbs Down</button>: {{ movie.thumbs_down }}</p>
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
      currentMovie: {},
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
    thumbsUp: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      var params = {
        params: { thumbs: "up" },
      };
      axios
        .patch(`/api/movies/${this.currentMovie.imdb_id}`, null, {
          params: { thumbs: "up" },
        })
        .then((response) => {
          this.currentMovie.thumbs_up += 1;
        });
    },
    thumbsDown: function (movie) {
      // console.log(movie);
      this.currentMovie = movie;
      var params = {
        params: { thumbs: "down" },
      };
      axios
        .patch(`/api/movies/${this.currentMovie.imdb_id}`, null, {
          params: { thumbs: "down" },
        })
        .then((response) => {
          this.currentMovie.thumbs_down += 1;
        });
    },
  },
};
</script>
