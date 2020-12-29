<template>
  <div class="home">
    <div class="container">
      <div class="row row-cols-1 row-cols-md-3 ">
        <div class="col mb-4 text-center " v-for="movie in movies">
          <div class="card h-100 border-0">
            <router-link v-bind:to="`/movies/${movie.imdb_id}`">
              <img :src="movie.image" />
            </router-link>
            <div class="card-body">
              <h3 class="card-title">{{ movie.title }}</h3>
              <h6 class="card-title">{{ movie.release_year }}</h6>
              <h6>
                <button type="button" class="btn btn-secondary" v-on:click="thumbsUp(movie)">Thumbs Up</button>:
                {{ movie.thumbs_up }}
              </h6>
              <h6>
                <button type="button" class="btn btn-secondary" v-on:click="thumbsDown(movie)">Thumbs Down</button>:
                {{ movie.thumbs_down }}
              </h6>
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
