// HTML
<template>
    <div id="movie-list">
        <div v-for="(movie, index) in filteredMovies" :key="index" class="movie">{{ movie.title }}</div>
    </div>
</template>
// Vue Script
 <script>
import genres from "../util/genres";
export default {
    data() {
        return {
            movies: [
                { title: "Pulp Fiction", genre: genres.CRIME },
                { title: "Home Alone", genre: genres.COMEDY },
                { title: "Austin Powers", genre: genres.COMEDY },
                { title: "Kill Bill", genre: genres.HORROR }
            ]
        };
    },
    props: ["genre", "time"],
    methods: {
        moviePassesGenreFilter(movie) {
            if (!this.genre.length) {
                return true;
            } else {
                return this.genre.find(genre => movie.genre === genre);
            }
        }
    },
    computed: {
        filteredMovies() {
            return this.movies.filter(this.moviePassesGenreFilter);
        }
    }
};
</script>