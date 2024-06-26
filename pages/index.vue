<template>
  <div>
    <h1 class="text-2xl font-bold mb-4 p-4">Filmes Populares</h1>
    <ul class="flex overflow-x-scroll space-x-4 p-4">
      <li v-for="movie in movies" :key="movie.id" class="bg-white shadow-md rounded-lg overflow-hidden flex-shrink-0 w-60">
        <div class="flex items-center">
          <img
            v-if="movie.poster_path"
            :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
            :alt="movie.title"
            class="w-full h-auto rounded-l-lg"
          />
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';

// Função para buscar filmes populares
const fetchMovies = async () => {
  const apiKey = '30822ee40eba4234096888d2fb5df8d2'; // Sua chave de API do TMDb
  const url = `https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}`;

  try {
    const response = await axios.get(url);
    return response.data.results; // Retorna os resultados dos filmes populares
  } catch (error) {
    console.error('Erro ao buscar filmes:', error);
    return []; // Retorna um array vazio em caso de erro
  }
};

// Ref para armazenar a lista de filmes
const movies = ref([]);

// Carrega os filmes populares ao montar o componente
onMounted(async () => {
  movies.value = await fetchMovies();
});
</script>
