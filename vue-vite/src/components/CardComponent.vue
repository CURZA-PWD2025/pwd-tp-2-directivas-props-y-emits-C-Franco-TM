<script setup>
import { defineProps, defineEmits } from 'vue';

// Prop que recibe la película
const props = defineProps({
  movie: {
    type: Object,
    required: true
  }
});

// Emitir el evento de actualización de likes
const emit = defineEmits(['update_likes']);

// Funcion para alternar el boton like
let liked = false;
const toggleLike = () => {
  if (!liked) {
    props.movie.likes += 1;
    liked = true;
  } else {
    props.movie.likes -= 1;
    liked = false;
  }
  emit('update_likes', props.movie.likes);
};
</script>

<template>
  <div class="card">
    <!-- Titulo y año de la pelicula -->
    <h2>{{ movie.titulo }} ({{ movie.anio }})</h2>

    <!-- Director de la pelicula-->
    <p>Director: {{ movie.director }}</p>

    <!-- Mostrar los géneros como una lista separada por comas -->
    <p>Género: {{ movie.generos.join(', ') }}</p>

    <!-- Imagen de la portada -->
    <p v-show="movie.portada">
      <img :src="movie.portada" alt="Portada" />
    </p>

    <!-- Mensaje si no hay portada -->
    <p v-show="!movie.portada">Portada no disponible</p>

    <!-- Botón para alternar los likes -->
    <button @click="toggleLike">Likes: {{ movie.likes }}</button>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 15px;
  margin: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
/*  width: 240px; /* Aseguramos que cada tarjeta tenga un ancho constante */
/*  box-sizing: border-box; /* Para que el padding no rompa el layout */
}

img {
  width: 240px;  /* Ancho */
  height: 360px; /* Altura */
  object-fit: cover; /* Ajustarse sin distorsionar */
  margin-top: 5px; /* Espacio arriba de la imagen */
}

button {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #e74c3c;
  border: none;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #000000;
}
</style>
