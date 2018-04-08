<template>
    <div id="app">

        <h1 style="text-align:center;">Various Movies</h1>

        <movie class="tile"
            v-for="movie in movies"
            v-bind:key="movie.id"
            v-bind:title="movie.title"
            v-bind:rating="movie.rating"
            v-bind:description="movie.description"
            v-bind:director="movie.director" >
        </movie>
    </div>
</template>

<script>
import axios from 'axios';
import Movie from "./components/Movie.vue";
import { key } from './scripts/config';

export default {
    name: "app",

    components: {
        Movie
    },

    data() {
        return {
            movies: [
                { id: 1, title: 'Pulp Fiction', rating: 9.5, description: 'A greate film', director: 'Quentin Tarrintino' },
                { id: 2, title: 'Casino', rating: 7.5, description: 'A violent film', director: 'Martin Scorcese' },
                { id: 3, title: 'Platoon', rating: 8.5, description: 'A war film', director: 'Oliver Stone' }
            ]
        }
    },

    created() {
        const query = `https://api.themoviedb.org/3/movie/upcoming?api_key=${key}&language=en-US&page=1`;
        axios(query)
            .then(response => console.log(response.data.results))
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
