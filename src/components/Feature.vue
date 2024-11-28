<script setup>
import axios from "axios";

const { data: nowPlaying } = await axios.get(`https://api.themoviedb.org/3/movie/now_playing?api_key=${import.meta.env.VITE_TMDB_KEY}`);
</script>

<template>
  <div class="feature-heading">
    <h1>🎬 Featured Movies 🎥</h1>
  </div>

  <div class="movie-container">
    <div v-for="movie in nowPlaying.results" :key="movie.id" class="movie-item" @click="getMovieDetails(movie.id)">
      <div class="movie-banners">
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" :alt="movie.title" />
      </div>
      <div class="movie-description">
        <h3>{{ movie.title }}</h3>
        <p>Release Date: {{ movie.release_date }}</p>
        <a :href="`https://www.youtube.com/results?search_query=${movie.title}+trailer`" target="_blank"
          class="trailer">Watch the Trailer</a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.feature-heading {
  font-family: 'Monoton', cursive;
  color: white;
  background: linear-gradient(to bottom, #323232, rgba(0, 0, 0, 0.639));
  text-align: center;
  padding: 30px;
}


.movie-item {
  margin: 15px;
  border-radius: 20px;
  width: 30%;
  height: 100%;
  overflow: hidden;
  transition: 0.3s;
  border: 3px solid #ffc1078d;
}

.movie-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 20px;
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