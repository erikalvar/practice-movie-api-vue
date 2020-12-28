
<template>
  <div class="home">
    <h1>Movie Search</h1>

    <input type="text" v-model="input">
    <button type="button" v-on:click="moviesSearch()" >
      Search
    </button>

    <p>{{ input }}</p>
    <p>{{ searches }}</p>

    <div v-for="movie in searches">
      <router-link v-bind:to="`/movies/${movie.imdb_id}`">
        <h1>{{ movie.title }}</h1>
      </router-link>
      <h1>{{ movie.title }}</h1>
      <p>{{ movie.release_year }}</p>
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