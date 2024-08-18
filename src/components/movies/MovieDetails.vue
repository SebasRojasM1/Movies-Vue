<template>
    <section class="movie-details">

      <div class="back-botton">
        <router-link to="/" class="botton">←</router-link>
      </div>

      <div class="container-info">
        <div class="poster-container">
          <img :src="movie?.Poster" :alt="movie?.Title">
        </div>
        
        <div class="info-movie">
          <h2>{{ movie?.Title }}</h2>
          <p><strong>Plot:</strong><br> {{ movie?.Plot }}</p>
          <p><strong>Genre:</strong><br> {{ movie?.Genre }}</p>
          <p><strong>Actors:</strong><br> {{ movie?.Actors }}</p>
          <p><strong>Language:</strong><br> {{ movie?.Language }}</p>
          <p><strong>Year:</strong><br> {{ movie?.Year }}</p>
          <p><strong>Runtime:</strong><br> {{ movie?.Runtime }}</p>
          <router-link to="/" class="back-link">Volver a la búsqueda</router-link>
        </div>
      </div>
      
    </section>
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
  
  <style scoped lang="scss">
  .movie-details {
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    padding: 20px;
    background-color: #f4f4f4;
    border: 5px solid $primary;
    border-radius: 13px;
    max-width: 800px;
    margin: 2% auto;

    .back-botton{
      .botton{
        background-color: $primary;
        border-radius: 50%;
        padding: 5px 7px;
        text-align: center;
        text-decoration: none;
        color: white;
        transition: 0.7s ease;  

        &:hover{
          background-color: #3b1577;
          transition: 0.7s ease;
        }
      }
    }

    .container-info{
      display: flex;
      flex-direction: row;
      align-items: center;

      .poster-container{
        width: 50%;
          img {
          max-width: 100%;
          height: auto;
          margin-bottom: 20px;
        }
      }

      .info-movie{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        text-align: center;
        width: 50%;

        h2 {
          margin-bottom: 20px;
        }
      
        .back-link{
          background-color: $primary;
          color: white;
          padding: 10px;
          text-decoration: none;
          border-radius: 15px;
          margin: 15px;
          transition: 0.7s ease;

          &:hover{
            background-color: #3b1577;
            transition: 0.7s ease;
          }
        }
      }
    }
  }

    
  
  
  </style>