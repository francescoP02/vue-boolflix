<template>

  <header class="d-flex">
    <h1>Boolflix</h1>
    <div>
      <div class="d-flex py-2">
        <input
          type="text"
          class="form-control col-6"
          id="search-text"
          placeholder="Search Movies or TV Shows"
          v-model="searchText"
          @keyup.enter="$emit('clickedSearch', searchText)"
        />
        <button
          type="button"
          class="btn btn-primary ms-2"
          @click="$emit('clickedSearch', searchText)"
        >
          Search
        </button>
      </div>
    </div>
  </header>

</template>

<script>
export default {
  name: "AppHeader",
  data: function () {
    return {
      searchText: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
@import "../style/common.scss";

header {
  background-color: $h-background;
  height: 60px;
  flex-direction: row;
  justify-content: space-around;

  h1 {
    color: red;
    text-transform: uppercase;
    align-items: center;
  }

}
</style>