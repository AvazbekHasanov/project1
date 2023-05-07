<template>
  <div class="movie-add-form">
    <h3>Yangi kino qo'shihs</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
        type="text"
        class="form-control new-movie-label"
        placeholder="Kino nomi"
        :value="name"
        v-on:input="name = $event.target.value" />
      <input
        type="number"
        class="form-control new-movie-label"
        placeholder="Necha marotiba ko'rilgan"
        :value="viuwers"
        v-on:input="viuwers = $event.target.value" />

      <button class="btn btn-outline-dark" type="submit" @click="addMovie">
        Qo'shish
      </button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      viuwers: ""
    };
  },
  methods: {
    addMovie() {
      if (!this.name || !this.viuwers) return;
      const newMovie = {
        name: this.name,
        viuwers: this.viuwers,
        like: false,
        favourite: false,
        id: Date.now()
      };
      this.$emit("createMovie", newMovie);
      this.name = "";
      this.viuwers = "";
    }
  }
};
</script>
<style>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 15px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
