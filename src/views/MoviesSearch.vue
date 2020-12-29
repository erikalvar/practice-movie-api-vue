<template>
  <div class="home">
    <div class="container text-center">
      <h1>Movie Title Search</h1>

      <div class="form-inline justify-content-center">
        <label for="exampleFormControlInput1">Movie Title:</label>
        <input
          type="text"
          class="form-control"
          id="exampleFormControlInput1"
          placeholder="Shrek"
          v-model="input"
        />
        <button type="button" class="btn btn-primary" v-on:click="moviesSearch()">
        Search
      </button>
      </div>
      <!-- <button type="button" class="btn btn-primary" v-on:click="moviesSearch()">
        Search
      </button> -->

      <!-- <p>{{ input }}</p>
      <p>{{ searches }}</p> -->

      <!-- <div v-for="movie in searches">
        <router-link v-bind:to="`/movies/${movie.imdb_id}`">
          <h1>{{ movie.title }}</h1>
        </router-link> -->
      <!-- <h1>{{ movie.title }}</h1> -->
      <!-- <p>{{ movie.release_year }}</p>
      </div> -->

      <div class="list-group" v-for="movie in searches">
        <!-- <a href="#" class="list-group-item list-group-item-action"
          >Dapibus ac facilisis in</a
        > -->
        <router-link
          class="list-group-item list-group-item-action"
          v-bind:to="`/movies/${movie.imdb_id}`"
        >
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.release_year }}</p>
        </router-link>
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
      searches: {},
      input: "",
    };
  },
  created: function () {
    // this.moviesIndex();
  },
  methods: {
    moviesSearch: function () {
      axios
        .get("api/searches/", {
          params: { title: this.input },
        })
        .then((response) => {
          this.searches = response.data;
          // console.log(this.searches);
        });
    },
  },
};
</script>
