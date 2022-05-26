<template>
  <div id="app">
    <header>
      <AppHeader @clickedSearch="performSearch"/>
    </header>
    <main>
      <AppLoading v-if="loading" />
      <AppMain v-else :moviesList="movieList" :serieList="seriesList"/>
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppLoading from "./components/AppLoading.vue";
import axios from "axios";
export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain,
    AppLoading,
  },
  data() {
    return {
      movieList: [],
      seriesList: [],
      filter: {
        genre: "",
        artist: "",
      },
      loading: false,
    }
  },
  methods: {
    performSearch(searchTerm) {
      this.loading = true;
      const params = {
            api_key: "ada2d065ca5348c690e937f411db9e54",
            lang: "en-US",
            page: 1,
            query: searchTerm,
      };
      axios
        .get("https://api.themoviedb.org/3/search/movie", { params })
        .then((resp) => {
          this.movieList = resp.data.results;
          this.movieList.forEach(item => {
            axios
              .get(`https://api.themoviedb.org/3/movie/${item.id}/credits`, {params} )
              .then((resp) => {
                item.cast = resp.data.cast.splice(0, 5);
                this.movieList.push(item);
              });
          });
          setTimeout(() => {
            this.loading = false;
          }, 1000);
          // this.movieList.forEach((element) => {
          // element.vote_average = "&starf;".repeat(
          // Math.ceil(element.vote_average / 2)
          // );
          // });
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", { params } )
        .then((resp) => {
          this.seriesList = resp.data.results;
          this.seriesList.forEach(item => {
            axios
              .get(`https://api.themoviedb.org/3/movie/${item.id}/credits`, {params} )
              .then((resp) => {
                item.cast = resp.data.cast.splice(0, 5);
                this.seriesList.push(item);
              });
          });
          setTimeout(() => {
            this.loading = false;
          }, 1000);
          // this.seriesList.forEach((element) => {
          // element.vote_average = "&starf;".repeat(
          // Math.ceil(element.vote_average / 2)
          // );
          // });
        });
    },
  },
  computed: {
  },
  
}
</script>

<style lang="scss">
@import "./style/variables.scss";
@import "./style/common.scss";
</style>
