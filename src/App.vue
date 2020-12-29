<template>
  <div id="app">
    <div id="nav">
      <!-- <h1>Movie Rating App</h1>
      <router-link to="/">Home</router-link> |
      <router-link to="/search">Search Movies</router-link> |
      <router-link to="/about">About</router-link> -->

      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <!-- <a class="navbar-brand" href="#">Movie-Rater</a> -->
        <router-link class="navbar-brand" to="/">
        <img src="../public/projector.png" width="30" height="30" class="d-inline-block align-top" alt="" loading="lazy">
        Movie-Rater</router-link>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNavDropdown"
          aria-controls="navbarNavDropdown"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav">
            <li class="nav-item active">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item active">
              <router-link class="nav-link" to="/search">Search Movies</router-link>
            </li>
            <li class="nav-item active">
              <router-link class="nav-link" to="/about">About</router-link>
            </li>
          </ul>
        </div>
      </nav>
    </div>
    <router-view />
  </div>
</template>

<style></style>
