<template>
  <AppLoading v-if="loading" />
  <div v-else class="container">
    <AppFilter @clickedSearch="performSearch($event)" />
    <h2 class="text-center col-12 py-2">Film</h2>
    <div class="row row-cols-2 row-cols-md-4 g-2">
      <MovieCard
        v-for="(item, index) in movieList"
        :key="index"
        :feature="item"
      />
    </div>
    <h2 class="text-center col-12 py-2">Serie TV</h2>
    <div class="row row-cols-2 row-cols-md-4 g-2">
      <SerieCard
        v-for="(item, index) in seriesList"
        :key="index"
        :feature="item"
      />
    </div>
  </div>
</template>

<script>
import MovieCard from "./MovieCard.vue";
import SerieCard from "./SerieCard.vue";
import AppLoading from "./AppLoading.vue";
import AppFilter from "./AppFilter.vue";
import axios from "axios";

export default {
  name: "AppMain",
  components: {
    MovieCard,
    AppLoading,
    AppFilter,
    SerieCard,
  },
  data() {
    return {
      movieList: [],
      seriesList: [],
      loading: false,
      filter: {
        genre: "",
        artist: "",
      },
    };
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
          setTimeout(() => {
            this.loading = false;
          }, 600);
        });

        axios
        .get("https://api.themoviedb.org/3/search/tv", { params } )
        .then((resp) => {
          this.seriesList = resp.data.results;
          setTimeout(() => {
            this.loading = false;
          }, 600);
        });
    },
  },
  computed: {},
  created() {},
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
@import "../style/common.scss";

</style>