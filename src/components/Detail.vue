<template>
    <div id="detail" v-if="movie">
        <movie-item :movie="movie">
            <div class="movie-details">
                <p class="movie-genre">{{movie.Genre}}</p>
                <p class="movie-plot">{{movie.Plot}}</p>
                <table>
                    <tr>
                        <td>Released date:</td>
                        <td>{{movie.Released}}</td>
                    </tr>
                    <tr>
                        <td>Running Time:</td>
                        <td>{{movie.Runtime}}</td>
                    </tr>
                    <tr>
                        <td>Director:</td>
                        <td>{{movie.Director}}</td>
                    </tr>
                    <tr>
                        <td>Cast:</td>
                        <td>{{movie.Actors}}</td>
                    </tr>
                </table>
            </div>
        </movie-item>
        <div class="home">
            <router-link :to="{name: 'home'}">Back to home</router-link>
        </div>
    </div>
</template>
<script>
import movieItem from "./MovieItem.vue";
export default {
    props: ["movies"],
    computed: {
        movie() {
            let movie = this.movies.find(
                movie => movie.id === this.$route.params.id
            );
            return movie ? movie.movie : null;
        }
    },
    components: {
        movieItem
    }
};
</script>
