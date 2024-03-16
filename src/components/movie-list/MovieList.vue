<template>
  <Box class="list-group">
    <MovieItem
        v-for="movie in movies"
        :movie="movie"
        :key="movie.id"
        @onToggle="$emit('onToggle',$event)"
        @onRemove="$emit('onRemove',movie.id)"
    />

  </Box>
</template>

<script>
import MovieItem from "@/components/movie-list-item/MovieItem.vue";
export default {
  components: {
    MovieItem,
  },
  props: {
    movies: {
      type: Array,
      required: true
    },
  }
}
</script>

<style scoped>

</style>