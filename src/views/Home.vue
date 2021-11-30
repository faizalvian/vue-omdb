<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>What you <strong>looking for?</strong></h2>
        </div>
      </div>
      <form @submit.prevent="SearchMovies()">
        <div class="row mt-3">
          <div class="col-lg-6 col-md-6 col-sm-12 mb-3">
            <input type="text" class="form-control" placeholder="Search movie..." v-model="search">
          </div>
          <div class="col-lg-6 col-md-6 col-sm-12">
            <button type="submit" class="btn btn-secondary">Search</button>
          </div>
        </div>
      </form>
      <div class="row mb-3">
        <div class="col-lg-3 col-md-3 col-sm-6 mt-4" v-for="movie in movies" :key="movie.imdbID">
          <router-link :to="'/movie/' + movie.imdbID" style="text-decoration: none">
            <div class="card bg-dark text-white">
              <img :src="movie.Poster" class="img-responsive" height="450">
              <div class="card-body">
                <h6 class="card-title text-center">{{movie.Title}} ({{movie.Year}})</h6>
              </div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import { ref } from "vue";
import env from '@/env.js'

export default {
  name: "Home",
  title:"VueMovie | Home",
  components: {
    Navbar
  },
  setup() {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = "";
        })
      }
    }
    return {
      search,
      movies,
      SearchMovies
    }
  }
};
</script>

<style>
  .card{
    max-height: 520px;
  }
  .card img{
    max-width: 100%;
  }
  h6{
    color: #fff;
  }
</style>