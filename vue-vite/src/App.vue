<script setup>
import { ref } from 'vue';
import CardComponent from './components/CardComponent.vue';
import moviesData from './resources/movies';

// Arreglo de películas
const movies = ref(moviesData);
</script>

<template>
  <div>
    <h1>PWD - Películas</h1>
    <div class="card-container">
      <div v-for="movie in movies" :key="movie.id">
        <CardComponent :movie="movie" @update_likes="updateLikes(movie.id, $event)" />
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  color: red;
}
.card-container {
  display: grid; /* Grid para distribuir las tarjetas */
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); /* Crea tantas columnas como sea necesario */
  padding: 0 16px; /* Espacio costado de las tarjetas */
  max-width: 1200px; /* Ancho maximo del contenedor */  
  margin-top: 20px; /* Espacio encima de las tarjetas */
}

</style>
