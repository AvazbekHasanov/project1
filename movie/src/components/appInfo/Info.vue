<template>
  <div class="app-info">
    <p class="fs-3 text-uppercase">Barcha kinolar soni: {{ allMoviesCount }}</p>
    <p class="fs-4 text-uppercase">
      Sevimli kinolar soni: {{ favouriteMoviesCount }}
    </p>
  </div>
</template>

<script>
export default {
  // name: "Info"
  props: {
    allMoviesCount: {
      type: Number,
      required: true
    },
    favouriteMoviesCount: {
      type: Number,
      required: true
    }
  }
};
</script>

<style scoped>
.app-info {
  padding: 1.5rem;
  border-radius: 4px;
  background-color: #fcfafc;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
