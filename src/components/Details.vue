<script setup>
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
const response = await axios.get(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${import.meta.env.VITE_TMDB_KEY}&append_to_response=videos`);
console.log(response.data);
</script>
<template>
    <div class="header-gap"></div>
    <div class="movie-detail">
        <img :src="`https://image.tmdb.org/t/p/w500${response.data.poster_path}`" alt="Movie Poster"
            class="movie-poster" />

        <div class="movie-details">
            <h1 class="movie-title">{{ response.data.original_title }}</h1>
            <p class="movie-overview">{{ response.data.overview }}</p>
            <p class="movie-release-date">Release Date: {{ response.data.release_date }}</p>
            <a class="movie-site" :href="response.data.homepage" target="_blank">Official Movie Site</a>
            <h2 class="trailers-title">Trailers</h2>
            <div class="trailers-container">
                <div v-for="trailer in response.data.videos.results" :key="trailer.id" class="trailer-tile">
                    <a :href="`https://www.youtube.com/watch?v=${trailer.key}`" target="_blank">
                        <img :src="`https://img.youtube.com/vi/${trailer.key}/hqdefault.jpg`" alt="Trailer"
                            class="trailer-thumbnail" />
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.header-gap {
    margin-bottom: 30px;
}

.movie-detail {
    font-family: 'Oswald', sans-serif;
    color: white;
    padding: 30px;
    background: linear-gradient(to bottom, #323232, rgba(0, 0, 0, 0.639));
    border-radius: 10px;
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-direction: row;
    gap: 30px;
}

.movie-poster {
    width: 250px;
    height: 375px;
    border-radius: 10px;
    object-fit: cover;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
}

.movie-details {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
}

.movie-title {
    font-family: 'Monoton', cursive;
    color: #ffcc00;
    font-size: 3rem;
    margin-bottom: 10px;
}

.movie-overview {
    font-size: 1.2rem;
    line-height: 1.6;
    margin-bottom: 20px;
    text-align: justify;
}

.movie-release-date {
    font-size: 1rem;
    margin-bottom: 20px;
    color: #ffcc00;
}

.movie-site {
    font-size: 1.1rem;
    display: inline-block;
    background: #ffcc00;
    color: black;
    padding: 10px 20px;
    border-radius: 5px;
    text-decoration: none;
    transition: background-color 0.3s, color 0.3s;
    margin-top: 20px;
}

.movie-site:hover {
    background: #ffc107;
    color: white;
}

.trailers-title {
    font-family: 'Monoton', cursive;
    color: #ffcc00;
    font-size: 2rem;
    margin-top: 40px;
    margin-bottom: 20px;
}

.trailers-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    gap: 15px;
}

.trailer-tile {
    width: 160px;
    border-radius: 10px;
    overflow: hidden;
    cursor: pointer;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
    transition: transform 0.3s;
}

.trailer-tile:hover {
    transform: scale(1.05);
}

.trailer-thumbnail {
    width: 100%;
    height: 90px;
    object-fit: cover;
    border-radius: 10px;
}
</style>