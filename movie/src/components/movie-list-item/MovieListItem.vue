<template>
  <li
    class="list-group-item d-flex jutify-content-between"
    :class="[{ like: movie.like }, { favourite: movie.favourite }]">
    <span class="list-group-item-label" @click="onlike">{{ movie.name }}</span>
    <input type="number" class="list-group-item-input" :value="movie.viuwers" />

    <div class="d-flex justify-content-center align-item-center">
      <button class="btn-cookie btn-sm" type="button" v-on:click="onFavourite">
        <i class="fas fa-cookie"></i>
      </button>

      <button class="btn-trash btn-sm" type="button" @click="onRemove">
        <i class="fas fa-trash"></i>
      </button>

      <i class="fas fa-star"></i>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    movie: {
      type: Object,
      required: true
    }
  },
  methods: {
    onlike() {
      this.$emit("onlike", this.movie.id);
    },
    onFavourite() {
      this.$emit("onFavourite", this.movie.id);
    },
    onRemove() {
      this.$emit("onRemove", this.movie.id);
    }
  }
};
</script>

<style>
.list-group-item {
  padding: 15px 20px;
  border-bottom: 1px solid #3d5a80;
}
.list-group-item:last-child {
  border-bottom: none;
}
.list-group-item span {
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
  width: 550px;
}
.list-group-item input {
  line-height: 35px;
  font-size: 20px;
  text-align: center;
  border: 0;
  outline: none;
}
.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}
.list-group-item .btn-cookie {
  color: #e09f3e;
}
.list-group-item .btn-trash {
  color: #e5383b;
}
.list-group-item .fa-star {
  width: 35px;
  height: 35px;
  text-align: center;
  line-height: 35px;
  font-size: 16px;
  color: #ffd700;
  transition: 0.3s all;
  transform: translateX(30px);
  opacity: 0;
}

.list-group-item.like .fa-star {
  opacity: 1;
  transform: translateX(0px);
}
.list-group-item.favourite .list-group-item-label,
.list-group-item.favourite .list-group-item-input {
  color: #e09f3e;
}
</style>
