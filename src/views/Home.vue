<template>
  <div class="home">
    <div class="container">
      <div class="row row-cols-1 row-cols-md-3 " >
        <div class="col mb-4 text-center " v-for="movie in movies">
          <div class="card h-100 border-0">
            <router-link v-bind:to="`/movies/${movie.imdb_id}`">
              <img :src="movie.image" />
            </router-link>
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <h7 class="card-title">{{ movie.release_year }}</h7>
              <p class="card-text">
                This is a longer card with supporting text below as a natural
                lead-in to additional content. This content is a little bit
                longer.
              </p>
            </div>
          </div>
        </div>
      </div>
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
