// HTML
<template>
    <div id="movie-list">
        <div class v-if="filteredMovies.length">
            <movie-item v-for="movie in filteredMovies" :movie="movie.movie" :key="movie.id"></movie-item>
        </div>
        <div class="no-results" v-else-if="movies.length">No Results.</div>
        <div class="no-results" v-else>Loading...</div>
    </div>
</template>
// Vue Script
 <script>
import genres from "../util/genres";
import MovieItem from "./MovieItem.vue";
export default {
    props: ["genre", "time", "movies"],
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
};
</script>