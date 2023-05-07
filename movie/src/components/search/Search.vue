<template>
  <input
    type="text"
    class="form-control search-input"
    placeholder="Kinolarni qidirish"
    :value="term"
    @input="chageHandler" />
</template>
<script>
export default {
  props: {
    updatedTermHandler: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      term: ""
    };
  },
  methods: {
    chageHandler(e) {
      this.term = e.target.value;
      this.updatedTermHandler(this.term);
    }
  }
};
</script>
<style scoped>
.search-input {
  margin-top: 2rem;
  padding: 1.5rem;
  margin-bottom: 1rem;
  background-color: #fcfaf5;
  margin-bottom: 1rem;
  border-radius: 15px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
