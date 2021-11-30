<template>
    <div>
        <Navbar />
        <div class="container">
            <h2 class="my-3">Movie Details</h2>
            <div class="card my-3">
                <div class="row g-0">
                    <div class="col-md-4">
                    <img :src="movie.Poster" class="img-fluid rounded-start">
                    </div>
                    <div class="col-md-8">
                        <div class="card-body">
                            <table class="table">
                                <thead>
                                    <tr>
                                        <th>Informations</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>
                                            <strong>Title : </strong>
                                            {{movie.Title}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Year : </strong>
                                            {{movie.Year}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Released : </strong>
                                            {{movie.Released}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Genre : </strong>
                                            {{movie.Genre}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Director(s) : </strong>
                                            {{movie.Director}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Writer(s) : </strong>
                                            {{movie.Writer}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Actors : </strong>
                                            {{movie.Actors}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Language : </strong>
                                            {{movie.Language}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Country : </strong>
                                            {{movie.Country}}
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>
                                            <strong>Plot : </strong>
                                            {{movie.Plot}}
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/Navbar';
import { ref,onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
    name:"MovieDetail",
    title:"VueMovie | Detail Movie",
    components:{
        Navbar
    },
    setup() {
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data => {
                movie.value = data;
            })
        });

        return{
            movie
        }
    }
}
</script>

<style>
    .card img{
        width: 100%;
    }
    .card{
        padding: 5px;
    }
    .card-text{
        text-align: justify;
    }
</style>