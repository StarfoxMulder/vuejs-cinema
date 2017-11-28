<template>
  <div id="movie-list">  

    <div v-if="filteredMovies.length">
      <movie-item v-for="movie in filteredMovies" 
                  v-bind:movie="movie.movie" 
                  v-bind:sessions="movie.sessions"
                  v-bind:day="day"
      ></movie-item>
    </div>

    <div v-else-if="movies.length" class="no-results">
      No Results.
    </div>

    <div v-else class="no-results">
      Loading....
    </div>

  </div>
</template>

<script>
  import genres from '../util/genres';
  import MovieItem from './MovieItem.vue';

  export default {

    props: ['genre', 'time', 'movies', 'day'],
    methods: {
      moviePassesGenreFilter(movie) {
        if (!this.genre.length) {
          return true;
        } else {
          // Movies have a comma separated list of genres, so this
          //creates an array containing all of a movie's genres
          let movieGenres = movie.movie.Genre.split(', ');
          let matched =  true;
          this.genre.forEach(genre => {
            if (movieGenres.indexOf(genre) === -1) {
              matched = false;
            }
          });
          return matched;
        }
      }
    },
    computed: {
      filteredMovies() {
        return this.movies.filter(this.moviePassesGenreFilter);
      }
    },
    components: {
      MovieItem
    },
    created() {
      console.log("this.$moment in MovieList");
      console.log(this.$moment);
    }
  }
</script>

<style>
/*****
*
* Original Dummy Data for movies:
          { title: 'Pulp Fiction', genre: genres.CRIME},
          { title: 'Dumb & Dumber', genre: genres.COMEDY},
          { title: 'The Lion King', genre: genres.ANIMATION},
          { title: 'Labrynth', genre: genres.FANTASY},
          { title: 'Why We Fight', genre: genres.DOCUMENTARY},
          { title: 'Jason Takes Manhattan', genre: genres.HORROR},
          { title: 'Clueless', genre: genres.COMEDY}
*
*/

</style>
