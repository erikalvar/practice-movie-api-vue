<template>
  <div class="movies-show">
    <h1>Movie Details</h1>

   
      <img :src="movie.image">
      <h1>{{ this.movie.title }}</h1>
      <p>{{ movie.release_year }}</p>
      <p>{{ movie.description }}</p>
      <p><button v-on:click="thumbsUp()">Thumbs Up</button>: {{ movie.thumbs_up }}</p>
      <p><button v-on:click="thumbsDown()">Thumbs Down</button>: {{ movie.thumbs_down }}</p>

      <!-- <button v-on:click="thumbsUp()">Thumbs Up!</button>
      <button v-on:click="thumbsDown()">Thumbs Down!</button> -->
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
    thumbsUp: function (movie) {
      var params = {
        params: { thumbs: "up" },
      };
      axios
        .patch(`/api/movies/${this.movie.imdb_id}`, null, {
          params: { thumbs: "up" },
        })
        .then((response) => {
          this.movie.thumbs_up += 1;
        });
    },
    thumbsDown: function (movie) {
      var params = {
        params: { thumbs: "up" },
      };
      axios
        .patch(`/api/movies/${this.movie.imdb_id}`, null, {
          params: { thumbs: "down" },
        })
        .then((response) => {
          this.movie.thumbs_down += 1;
        });
    },
  },
};
</script>
