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
import Movie from "./components/Movie.vue";

export default {
    name: "app",

    components: {
        Movie
    },

    data: function() {
        return {
            movies: [
                { id: 1, title: 'Pulp Fiction', rating: 9.5, description: 'A greate film', director: 'Quentin Tarrintino' },
                { id: 2, title: 'Casino', rating: 7.5, description: 'A violent film', director: 'Martin Scorcese' },
                { id: 3, title: 'Platoon', rating: 8.5, description: 'A war film', director: 'Oliver Stone' }
            ]
        }
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
