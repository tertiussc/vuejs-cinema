<template>
    <div id="movie-filter">
        <h2>Filter results</h2>
        <h3>By Time of Day</h3>
        <div class="filter-group">
            <check-filter
                v-for="(time, index) in times"
                category="time"
                :key="index"
                v-bind:title="time"
            ></check-filter>
        </div>
        <h3>By Genre</h3>
        <div class="filter-group">
            <check-filter
                v-for="(genre, index) in genres"
                category="genre"
                :key="index"
                v-bind:title="genre"
            ></check-filter>
        </div>
    </div>
</template>
<script>
import genres from "../util/genres";
import times from "../util/times";
import CheckFilter from "./CheckFilter.vue";
export default {
    data() {
        return {
            genres,
            times
        };
    },
    components: {
        CheckFilter
    }
};
</script>
