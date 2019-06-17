// HTML
<template>
    <div id="movie-list">
        <div class v-if="filteredMovies.length">
            <movie-item
                v-for="movie in filteredMovies"
                :movie="movie.movie"
                :sessions="movie.sessions"
                :day="day"
                :time="time"
                :key="movie.id"
            ></movie-item>
        </div>
        <div class="no-results" v-else-if="movies.length">No Results.</div>
        <div class="no-results" v-else>Loading...</div>
    </div>
</template>
// Vue Script
 <script>
import genres from "../util/genres";
import times from "../util/times";
import MovieItem from "./MovieItem.vue";
export default {
    props: ["genre", "time", "movies", "day"],
    methods: {
        moviePassesGenreFilter(movie) {
            if (!this.genre.length) {
                return true;
            } else {
                let movieGenres = movie.movie.Genre.split(", ");
                let matched = true;
                this.genre.forEach(genre => {
                    if (movieGenres.indexOf(genre) === -1) {
                        matched = false;
                    }
                });
                return matched;
            }
        },
        sessionPassesTimeFilter(session) {
            if (!this.day.isSame(this.$moment(session.time), "day")) {
                return false;
            } else if (this.time.length === 0 || this.time.length === 2) {
                return true;
            } else if (this.time[0] === times.AFTER_6PM) {
                return this.$moment(session.time).hour() >= 18;
            } else {
                return this.$moment(session.time).hour() < 18;
            }
        }
    },
    computed: {
        filteredMovies() {
            return this.movies
                .filter(this.moviePassesGenreFilter)
                .filter(movie =>
                    movie.sessions.find(this.sessionPassesTimeFilter)
                );
        }
    },
    components: {
        MovieItem
    }
};
</script>