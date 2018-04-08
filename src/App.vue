<template>
    <div id="app">

        <h1 style="text-align:center;">Upcoming Movies</h1>

        <movie class="tile"
            v-for="movie in movies"
            v-bind:key="movie.id"
            v-bind:title="movie.title"
            v-bind:rating="movie.vote_average"
            v-bind:description="movie.overview"
            v-bind:mpaa="movie.mpaa"
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
            movies: []
        }
    },

    created() {
        axios(`https://api.themoviedb.org/3/movie/upcoming?api_key=${key}&language=en-US&include_adult=false&page=1`)
            .then(response => {
                response.data.results.forEach((element, index) => {
                    axios(`https://api.themoviedb.org/3/movie/${element.id}?api_key=${key}&language=en-US&append_to_response=credits,release_dates`)
                        .then(response => {

                            // Build the movie object
                            let movie = {};
                            movie.budget = response.data.budget;
                            movie.homepage = response.data.homepage;
                            movie.imdb_id = response.data.imdb_id;
                            movie.overview = response.data.overview;
                            movie.popularity = response.data.popularity;
                            movie.poster_path = response.data.poster_path;
                            movie.release_date = response.data.release_date;
                            movie.revenue = response.data.revenue;
                            movie.runtime = response.data.runtime;
                            movie.status = response.data.status;
                            movie.tagline = response.data.tagline;
                            movie.title = response.data.title;
                            movie.vote_average = response.data.vote_average;
                            movie.vote_count = response.data.vote_count;
                            movie.trailer = '';

                            // Find the director in the crew array property
                            for (let member of response.data.credits.crew) {
                                if (member.job === 'Director') {
                                    movie.director = member.name;
                                    break;
                                }
                            }

                            // Find the mpaa rating
                            movie.mpaa = 'NR';
                            for (let country of response.data.release_dates.results) {
                                if (country.iso_3166_1 === 'US') {
                                    var certifications = country.release_dates;
                                    for (let item of certifications) {
                                        var mpaa = item.certification;
                                        if (mpaa !== '') {
                                            movie.mpaa = mpaa;
                                            break;
                                        }
                                    }
                                }
                            }

                            console.log(response.data);
                            this.movies.push(movie);
                        }
                    )
                    .catch(err => console.error(err))
                })
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
