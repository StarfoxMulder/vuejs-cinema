<template>
  <div class="movie">
    <div class="movie-col-left">
      <img v-bind:src="movie.Poster" />
    </div>
    <div class="movie-col-right">
      <div class="movie-title">
        <h2>{{ movie.Title }}</h2>
        <span class="movie-rating">{{ movie.Rated }}</span>
      </div>
      <div class="movie-sessions">
        <div v-for="session in filteredSessions(sessions)" class="session-time-wrapper">
          <div class="session-time"> {{ formatSessionTime(session.time) }} </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

  export default {
  // The prop is an alias for the v-bind "movie.movie" in MovieList
  // when it was v-bind:movie="movie" the template here was movie.movie.Title
  // but now that the bind is movie.movie, we only need to reference 
  // the alias of movie which is bound to each iteration of MovieItem
  // within it's parent MovieList
    props: ['movie', 'sessions', 'day'],
    methods: {
      formatSessionTime(raw) {
        return this.$moment(raw).format('h:mm A');
      },
      filteredSessions(sessions) {
        return sessions.filter(session => {
          return this.$moment(session.time).isSame(this.day, 'day')
        })
      }
    }

  }
</script>

<style>
/*****
* Original Dummy Data for movies:
    { title: 'Pulp Fiction', genre: genres.CRIME},
    { title: 'Dumb & Dumber', genre: genres.COMEDY},
    { title: 'The Lion King', genre: genres.ANIMATION},
    { title: 'Labrynth', genre: genres.FANTASY},
    { title: 'Why We Fight', genre: genres.DOCUMENTARY},
    { title: 'Jason Takes Manhattan', genre: genres.HORROR},
    { title: 'Clueless', genre: genres.COMEDY}
*/

</style>
