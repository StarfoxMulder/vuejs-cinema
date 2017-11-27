<template>
  <div id="movie-list">
    <movie-item v-for="movie in filteredMovies" v-bind:movie="movie.movie"></movie-item>
  </div>
</template>

<script>
  import genres from '../util/genres';
  import MovieItem from './MovieItem.vue';

  export default {

    props: ['genre', 'time', 'movies'],
    methods: {
      moviePassesGenreFilter(movie) {
        if (!this.genre.length) {
          return true;
        } else {
          // Movies have a comma separated list of genres, so this
          //creates an array containing all of a movie's genres
          let movieGenres = movie.movie.Genre.split(', ');
          console.log("Logging movie.movie.Genre");
          console.log(movie.movie.Genre);
          console.log("Logging movieGenres");
          console.log(movieGenres);
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
