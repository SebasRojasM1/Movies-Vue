<template>
    <div class="movie-details">
      <h2>{{ movie?.Title }}</h2>
      <img :src="movie?.Poster" :alt="movie?.Title">
      <p><strong>Type:</strong> {{ movie?.Type }}</p>
      <p><strong>Year:</strong> {{ movie?.Year }}</p>
      <router-link to="/" class="back-link">Volver a la búsqueda</router-link>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import HTTP from '@/api/client-http';
  import type { Movie } from '@/model/movie.model';
  
  const route = useRoute();
  const movieId = route.params.id as string;
  
  const movie = ref<Movie>();
  
  onMounted(async () => {
    const response = await HTTP.get('', {
      params: {
        i: movieId
      }
    });
    movie.value = response.data;
  });
  </script>
  
  <style scoped>
  .movie-details {
    padding: 20px;
    background-color: #f4f4f4;
    border-radius: 8px;
    max-width: 600px;
    margin: 20px auto;
  }
  
  .movie-details h2 {
    margin-bottom: 20px;
  }
  
  .movie-details img {
    max-width: 100%;
    height: auto;
    margin-bottom: 20px;
  }
  </style>