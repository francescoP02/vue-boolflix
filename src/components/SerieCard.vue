<template>
  <div class="col">
    <div class="feature-card p-2 text-center">
      <img class="img-fluid" :src="`https://image.tmdb.org/t/p/w342${feature.poster_path}`" />

      <h2 class="feature-title fw-bold mt-3">{{ feature.name }}</h2>
      <p>{{ feature.original_name }}</p>
      <div>
        <FlagIcons :languageCode="feature.original_language" />
        <div> {{ feature.vote_average }} &star; </div>
      </div>

    </div>
  </div>
</template>

<script>
import FlagIcons from "./FlagIcons.vue";

export default {
  name: "SerieCard",
  props: {
    feature: Object,
  },
  components: {
    FlagIcons,
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
@import "../style/common.scss";

</style>