<template>
  <div class="col">

    <div class="img-card" :class="{ 'no-image': feature.poster_path === null }">
      <img class="img-fluid" :src="`https://image.tmdb.org/t/p/w342${feature.poster_path}`" />
    </div>

    <div class="feature-card p-2 text-center">
      <ul>
        <li>{{ feature.title }}</li>
        <li>{{ feature.original_title }}</li>
        <li><FlagIcons :languageCode="feature.original_language" /></li>
        <li>        
          <span
          v-if="feature.vote_average"
          v-html="feature.vote_average"
          ></span>
        </li>
        <li class="ms-overview">{{feature.overview}}</li>
      </ul>

    </div>
  </div>
</template>

<script>
import FlagIcons from "./FlagIcons.vue";

export default {
  name: "MovieCard",
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

.feature-card {
  .ms-overview {
    height: 100px;
    white-space: wrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
}

</style>