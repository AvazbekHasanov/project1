<template>
  <ul class="movie-list list-group">
    <MovieListItem
      v-for="movie in movies"
      :movie="movie"
      :key="movie.id"
      @onlike="$emit('onlike', movie.id)"
      @onFavourite="$emit('onFavourite', movie.id)"
      @onRemove="$emit('onRemove', $event)" />
  </ul>
</template>

<script>
import MovieListItem from "../movie-list-item/MovieListItem.vue";

export default {
  components: { MovieListItem },
  props: {
    movies: {
      typeof: Array,
      required: true
    }
  }
};
</script>
<style scoped>
.movie-list {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 15px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
