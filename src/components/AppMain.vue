<template>
<main>
  <div class="container">
    <h2 class="text-center col-12 py-2">Film</h2>
    <div class="row row-cols-2 row-cols-md-5 g-2">
      <MovieCard
        v-for="(item, index) in moviesList"
        :key="index"
        :feature="item"
        class="ms-card"
      />
    </div>
    <h2 class="text-center col-12 py-2">Serie TV</h2>
    <div class="row row-cols-2 row-cols-md-5 g-2">
      <SerieCard
        v-for="(item, index) in serieList"
        :key="index"
        :feature="item"
        class="ms-card"
      />
    </div>
  </div>
</main>
</template>

<script>
import MovieCard from "./MovieCard.vue";
import SerieCard from "./SerieCard.vue";

export default {
  name: "AppMain",
  components: {
    MovieCard,
    SerieCard,
},
    props: {
    moviesList: Object,
    serieList: Object,
  },
  created() {},
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
@import "../style/common.scss";

main {
  background-color: $m-background;
  min-height: calc(100vh - 60px);

  div {
    color: white;
    text-transform: uppercase;
  }
  
  .ms-card {
    height: 100%;
  }
}
</style>