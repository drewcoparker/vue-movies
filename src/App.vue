<template>
    <div id="app">

        <h1 style="text-align:center;">Various Movies</h1>

        <movie class="tile"
            v-for="movie in movies"
            v-bind:key="movie.id"
            v-bind:title="movie.title"
            v-bind:rating="movie.vote_average"
            v-bind:description="movie.overview"
            v-bind:director="movie.director" >
        </movie>
    </div>
</template>

<script>
import axios from 'axios';
import Movie from "./components/Movie.vue";
import { query } from './scripts/config';

export default {
    name: "app",

    components: {
        Movie
    },

    data() {
        return {
            movies: []
        }
    },

    created() {

        axios(query)
            .then(response => {
                this.movies = response.data.results
            })
            .catch(error => console.error(error))
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /* text-align: center; */
    color: #2c3e50;
    margin-top: 60px;
}

.tile {
    display: inline-block;
    padding: 1.5rem;
}
</style>
