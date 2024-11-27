<script setup>
import axios from 'axios';
import { useRouter } from 'vue-router';
import { ref } from 'vue';

const genres = [
    { genre: 'Action', id: 28 },
    { genre: 'Adventure', id: 12 },
    { genre: 'Animation', id: 16 },
    { genre: 'Comedy', id: 35 },
    { genre: 'Drama', id: 18 }
];

const selectedGenre = ref(null);
const moviesToShow = ref([]);
const router = useRouter();

async function fetchMovies() {
    if (selectedGenre.value) {
        const { data } = await axios.get(
            `https://api.themoviedb.org/3/discover/movie?api_key=${import.meta.env.VITE_TMDB_KEY}&with_genres=${selectedGenre.value}`
        );
        moviesToShow.value = data.results.slice(0, 9);
    }
}

function getMovieDetails(id) {
    router.push(`/movies/${id}`);
}

</script>

<template>
    <div class="genre-heading">
        <h1>🎬 Featured Movies by Genre 🎥</h1>
    </div>

    <div class="genre-selector">
        <select v-model="selectedGenre" @change="fetchMovies">
            <option value="" disabled>Select a Genre</option>
            <option v-for="genre in genres" :key="genre.id" :value="genre.id">
                {{ genre.genre }}
            </option>
        </select>
    </div>

    <div class="movie-container">
        <div v-for="movie in moviesToShow" :key="movie.id" class="movie-item" @click="getMovieDetails(movie.id)">
            <div class="movie-banners">
                <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" :alt="movie.title" />
            </div>
            <div class="movie-description">
                <h3>{{ movie.title }}</h3>
                <p>Release Date: {{ movie.release_date }}</p>
                <a :href="`https://www.youtube.com/results?search_query=${movie.title}+trailer`" target="_blank"
                    class="trailer">
                    Watch the Trailer
                </a>
            </div>
        </div>
    </div>
</template>

<style scoped>
.genre-heading {
    font-family: 'Monoton', cursive;
    color: white;
    background: linear-gradient(to bottom, #323232, rgba(0, 0, 0, 0.639));
    text-align: center;
    padding: 30px;
}

.genre-selector {
    display: flex;
    justify-content: center;
    margin: 20px 0;
    width: 100%;
}

.genre-selector select {
    padding: 12px;
    font-size: 1.1rem;
    border-radius: 5px;
    background-color: #ffcc002f;
    color: black;
    border: 2px solid #ffcc00;
    width: 250px;
    transition: background-color 0.3s, border 0.3s;
}

.genre-selector select:hover {
    background-color: #ffcc002f;
}

.movie-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 20px;
}

.movie-item {
    margin: 15px;
    border-radius: 20px;
    width: 30%;
    height: 100%;
    overflow: hidden;
    transition: 0.3s;
    border: 3px solid #ffc1078d;
    cursor: pointer;
}

.movie-banners img {
    width: 100%;
    height: 500px;
    transition: 0.3s;
}

.movie-item:hover {
    transform: scale(1.03);
}

.movie-banners img:hover {
    filter: brightness(50%);
}

.movie-description {
    font-family: 'Oswald', sans-serif;
    padding: 20px;
    color: white;
    background-color: rgba(28, 20, 20, 0.731);
    text-align: center;
}

.trailer {
    display: inline-block;
    background: #ffcc00;
    color: black;
    padding: 10px 20px;
    border-radius: 5px;
    text-decoration: none;
    margin-top: 10px;
    transition: 0.3s;
}

.trailer:hover {
    background: #ffc107;
    color: white;
}
</style>
