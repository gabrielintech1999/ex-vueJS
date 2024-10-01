<template>
    <div>
      <h1>Movie Search</h1>
      <input type="text" v-model="query" @keyup.enter="searchMovies" placeholder="Search for a movie" />
      <div v-if="movies.length">
        <div v-for="movie in movies" :key="movie.id">
          <h3>{{ movie.title }}</h3>
          <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="Movie poster" />
          <p>{{ movie.overview }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  export default {
    setup() {
      const query = ref('');
      const movies = ref([]);
  
      const searchMovies = async () => {
        if (query.value.trim()) {
          try {
            const response = await fetch(
              `https://api.themoviedb.org/3/search/movie?api_key=0d0b8ce3b08f5975324325568402e29d&query=${query.value}`
            );
            const data = await response.json();
            movies.value = data.results;
          } catch (error) {
            console.error("Error fetching movies:", error);
          }
        }
      };
  
      return {
        query,
        movies,
        searchMovies,
      };
    },
  };
  </script>