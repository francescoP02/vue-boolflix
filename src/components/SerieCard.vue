<template>
  <div class="col">

    <div class="card">
      <div class="img-card" :class="{ 'no-image': feature.poster_path === null }">
        <img v-if="feature.poster_path != null " class="img-fluid" :src="`https://image.tmdb.org/t/p/w342${feature.poster_path}`" />
        <!-- <img v-else class="ms-noimg img-fluid" src="../assets/default_image_01.png" alt=""> -->
        <div v-else class="ms-noimg"></div>
      </div>

      <div class="feature-card p-2 ">
        <ul>
          <li>{{ feature.name }}</li>
          <li  v-if="feature.original_name != feature.name" >{{ feature.original_name }}</li>
          <li><FlagIcons :languageCode="feature.original_language" /></li>
          <li>        
            <span class="ms-star"><i v-for="n in 5" :key="n" class="fa-star" :class="n <= filledStars ? 'fas' : 'far'"></i></span>
          </li>
          <li class="ms-overview">{{feature.overview}}</li>
        </ul>

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
  computed: {
    filledStars() {
      return Math.ceil(this.feature.vote_average / 2);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
@import "../style/common.scss";
@import '~@fortawesome/fontawesome-free/css/all.min.css';

.card {
  height: 100%;

  .img-card {
    position: relative;
    min-height: 100%;

    .ms-noimg {
    height: 100%;
    background-image: url(../assets/default_image_01.png);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    }
  }

  .feature-card {
  display: none;

    .ms-overview {

      height: 100px;
      white-space: wrap;
      overflow: hidden;
      text-overflow: ellipsis;

    }
  }

  &:hover {
    .feature-card {
      display: block;
      position: absolute;
      top: 0;
      left: 0;
      background-color: rgba(black, 0.8);
      width: 100%;
      height: 100%;
      color: white;

      .ms-star {
        color: yellow;
      }
    }
  }
}
</style>