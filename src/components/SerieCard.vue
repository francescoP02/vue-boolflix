<template>
  <div class="col">

    <div class="card">
      <div class="img-card" :class="{ 'no-image': feature.poster_path === null }">
        <img v-if="feature.poster_path != null " class="img-fluid" :src="`https://image.tmdb.org/t/p/w342${feature.poster_path}`" />
        <img v-else class="ms-noimg img-fluid" src="../assets/default_image_01.png" alt="">
      </div>

      <div class="feature-card p-2 ">
        <ul>
          <li>{{ feature.title }}</li>
          <li  v-if="feature.original_title != feature.title" >{{ feature.original_title }}</li>
          <li><FlagIcons :languageCode="feature.original_language" /></li>
          <li>        
            <span class="ms-star"><i v-for="n in 5" :key="n" :class="n <= filledStars ? 'fas fa-star' : 'far fa-star'"></i></span>
          </li>
          <li class="ms-overview">{{feature.overview}}</li>
          <li>
            <ul class="ms-cast">
              <li>Cast:</li>
              <li v-for="(actor, index) in feature.cast" :key="index">
                {{ actor.name }}
              </li>
            </ul>
          </li>
        </ul>

      </div>
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
.card {

  height: 100%;

  .img-card {
    position: relative;
    min-height: 100%;

    .ms-noimg {
    height: 100%;
    }

  }
  .feature-card {

  display: none;
  color: white;

    .ms-overview {

      height: 100px;
      white-space: wrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .ms-cast {
      font-size: .8rem;
    }
  }
  &:hover {
    .feature-card {
      display: block;
      position: absolute;
      top: 0;
      left: 0;
      background-color: black;
      width: 100%;
      height: 100%;

      .ms-star {
        color: yellow;
      }

    }
  }
}
</style>