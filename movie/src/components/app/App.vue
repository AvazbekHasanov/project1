<template>
  <div id="app font-monospace">
    <div class="content">
      <Info
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-pannel">
        <Search :updatedTermHandler="updatedTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter" />
      </div>
      <MovieList
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onlike="onlikeHandler"
        @onFavourite="onFavouriteHandler"
        @onRemove="onRemoveHandler" />
      <AddMovie @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import Search from "../search/Search.vue";
import Info from "../appInfo/Info.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import MovieList from "../movieList/MovieList.vue";
import AddMovie from "../movie-add-form/AddMuvie.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Search,
    Info,
    AppFilter,
    MovieList,
    AddMovie
  },
  // mounted() {
  //   this.fetchMovie();
  // },
  data() {
    return {
      movies: [],
      term: "",
      filter: ""
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onlikeHandler(id) {
      this.movies.map(item => {
        if (item.id == id) {
          item.like = !item.like;
        } else {
          return id;
        }
      });
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(c => c.id != id);
    },
    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr;
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1);
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter(c => c.like);
        case "mostViuwers":
          return arr.filter(c => c.viuwers > 500);

        default:
          return arr;
      }
    },
    onFavouriteHandler(id) {
      this.movies.map(item => {
        if (item.id == id) {
          item.favourite = !item.favourite;
        } else {
          return id;
        }
      });
    },
    updatedTermHandler(term) {
      this.term = term;
    },
    updateFilterHandler(filter) {
      this.filter = filter;
    },
    async fetchMovie() {
      try {
        const { data } = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );

        const newArr = data.map(item => ({
          id: item.id,
          name: item.title,
          like: false,
          favourite: false,
          viuwers: item.id * 45
        }));
        console.log(newArr);
        this.movies = newArr;
      } catch (error) {
        alert(error.message);
      }
    }
  },
  mounted() {
    this.fetchMovie();
  }
};
</script>
<style>
.app {
  height: 100vh;
  color: #000;
}
.content {
  width: 1000px;
  min-height: 700px;
  background-color: white;
  margin: auto;
  padding: 5rem 0;
}
.search-pannel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 15px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
