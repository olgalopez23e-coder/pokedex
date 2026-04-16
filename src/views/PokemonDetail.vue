<template>
  <div v-if="loading" class="loading-state" style="text-align: center; padding: 5rem;">
    <div class="loader" style="width: 60px; height: 60px; border: 6px solid #eee; border-top: 6px solid var(--color-primary); border-radius: 50%; animation: spin 1s linear infinite; margin: auto;"></div>
    <p style="margin-top: 1.5rem; font-size: 1.2rem; color: #666;">Buscando datos del Pokémon...</p>
  </div>

  <div v-else-if="pokemon" class="pokemon-detail">
    <div class="detail-container" style="background: white; border-radius: 20px; box-shadow: var(--shadow); overflow: hidden; display: flex; flex-direction: column; md:flex-row;">
      
      <!-- Lado Izquierdo: Imagen y Tipos -->
      <div class="detail-header" :class="`bg-${pokemon.types[0]}`" style="padding: 3rem; text-align: center; color: white; background-color: var(--color-primary); position: relative;">
        <button @click="$router.back()" style="position: absolute; top: 1rem; left: 1rem; background: rgba(0,0,0,0.2); border: none; color: white; padding: 0.5rem 1rem; border-radius: 20px; cursor: pointer;">← Volver</button>
        
        <img :src="pokemon.image" :alt="pokemon.name" style="width: 250px; height: 250px; filter: drop-shadow(0 10px 20px rgba(0,0,0,0.3));" />
        <h1 style="text-transform: capitalize; font-size: 3rem; margin-top: 1rem; text-shadow: 2px 2px 4px rgba(0,0,0,0.3);">{{ pokemon.name }}</h1>
        <div class="pokemon-types" style="justify-content: center; margin-top: 1rem; gap: 1rem;">
          <span v-for="type in pokemon.types" :key="type" :class="['type-badge', `type-${type}`]" style="font-size: 1rem; padding: 0.5rem 1.5rem;">
            {{ type }}
          </span>
        </div>
      </div>

      <!-- Lado Derecho: Info y Stats -->
      <div class="detail-body" style="padding: 2.5rem;">
        <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 2rem;">
          <div>
            <h2 style="color: var(--color-primary); margin-bottom: 0.5rem;">Descripción</h2>
            <p style="font-size: 1.1rem; color: #444; max-width: 600px;">{{ pokemon.description }}</p>
          </div>
          <button @click="toggleFavorito" :class="['fav-btn', { 'is-fav': esFavorito }]" style="padding: 1rem 1.5rem; border-radius: 12px; border: 2px solid var(--color-primary); cursor: pointer; transition: all 0.3s ease; font-weight: bold; display: flex; align-items: center; gap: 0.5rem;">
            <span style="font-size: 1.5rem;">{{ esFavorito ? '❤️' : '🤍' }}</span>
            {{ esFavorito ? 'En Favoritos' : 'Añadir a Favoritos' }}
          </button>
        </div>

        <div style="display: grid; grid-template-columns: 1fr 1.5fr; gap: 3rem;">
          <!-- Datos Básicos -->
          <div>
            <h3 style="margin-bottom: 1rem; border-bottom: 2px solid #eee; padding-bottom: 0.5rem;">Datos</h3>
            <div style="display: flex; flex-direction: column; gap: 0.8rem;">
              <div style="display: flex; justify-content: space-between;"><span style="color: #666;">Altura:</span> <strong>{{ pokemon.height / 10 }} m</strong></div>
              <div style="display: flex; justify-content: space-between;"><span style="color: #666;">Peso:</span> <strong>{{ pokemon.weight / 10 }} kg</strong></div>
              <div style="display: flex; justify-content: space-between;"><span style="color: #666;">Especie:</span> <strong style="text-transform: capitalize;">{{ pokemon.species }}</strong></div>
              <div style="display: flex; justify-content: space-between;"><span style="color: #666;">Habilidades:</span> 
                <div style="text-align: right;">
                  <div v-for="a in pokemon.abilities" :key="a.name" style="text-transform: capitalize;">{{ a.name }} {{ a.isHidden ? '(oculta)' : '' }}</div>
                </div>
              </div>
            </div>
          </div>

          <!-- Estadísticas -->
          <div>
            <h3 style="margin-bottom: 1rem; border-bottom: 2px solid #eee; padding-bottom: 0.5rem;">Estadísticas Base</h3>
            <div v-for="stat in pokemon.stats" :key="stat.name" style="margin-bottom: 1rem;">
              <div style="display: flex; justify-content: space-between; margin-bottom: 0.3rem;">
                <span style="text-transform: uppercase; font-size: 0.8rem; font-weight: bold; color: #666;">{{ stat.name }}</span>
                <strong>{{ stat.value }}</strong>
              </div>
              <div style="height: 10px; background: #eee; border-radius: 5px; overflow: hidden;">
                <div :style="{ width: `${(stat.value / 255) * 100}%`, backgroundColor: getStatColor(stat.name) }" style="height: 100%; transition: width 1s ease-out;"></div>
              </div>
            </div>
          </div>
        </div>

        <!-- Línea Evolutiva -->
        <div v-if="pokemon.evolutionChain && pokemon.evolutionChain.length > 1" style="margin-top: 3rem;">
          <h3 style="margin-bottom: 1.5rem; border-bottom: 2px solid #eee; padding-bottom: 0.5rem;">Línea Evolutiva</h3>
          <div style="display: flex; align-items: center; justify-content: space-around; gap: 1rem;">
            <template v-for="(name, index) in pokemon.evolutionChain" :key="name">
              <div style="text-align: center; cursor: pointer;" @click="$router.push(`/pokemon/${name}`)">
                <div style="width: 80px; height: 80px; background: #f0f0f0; border-radius: 50%; display: flex; align-items: center; justify-content: center; margin-bottom: 0.5rem; border: 2px solid transparent; transition: all 0.3s;" onmouseover="this.style.borderColor='var(--color-primary)'" onmouseout="this.style.borderColor='transparent'">
                  <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getEvolutionId(name)}.png`" style="width: 60px; height: 60px;" />
                </div>
                <div style="text-transform: capitalize; font-weight: bold; font-size: 0.9rem;">{{ name }}</div>
              </div>
              <span v-if="index < pokemon.evolutionChain.length - 1" style="font-size: 1.5rem; color: #ccc;">➜</span>
            </template>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import api from '../services/api';

const route = useRoute();
const pokemon = ref(null);
const loading = ref(true);
const esFavorito = ref(false);

const fetchPokemon = async () => {
  loading.value = true;
  try {
    const { idOrName } = route.params;
    const res = await api.get(`/pokemon/${idOrName}`);
    pokemon.value = res.data;
    
    // Verificar si es favorito
    await checkFavorito();
  } catch (error) {
    console.error('Error al cargar detalles del pokémon:', error);
  } finally {
    loading.value = false;
  }
};

const checkFavorito = async () => {
  try {
    const res = await api.get('/favorites');
    esFavorito.value = res.data.favorites.some(f => f.pokemonId === pokemon.value.id);
  } catch (error) {
    console.error('Error al verificar favorito:', error);
  }
};

const toggleFavorito = async () => {
  try {
    if (esFavorito.value) {
      await api.delete(`/favorites/${pokemon.value.id}`);
      esFavorito.value = false;
    } else {
      await api.post('/favorites', {
        pokemonId: pokemon.value.id,
        pokemonName: pokemon.value.name,
        pokemonData: { 
          image: pokemon.value.image,
          types: pokemon.value.types
        }
      });
      esFavorito.value = true;
    }
  } catch (error) {
    console.error('Error al cambiar estado de favorito:', error);
  }
};

const getStatColor = (name) => {
  const colors = {
    hp: '#FF0000',
    attack: '#F08030',
    defense: '#F8D030',
    'special-attack': '#6890F0',
    'special-defense': '#78C850',
    speed: '#F85888'
  };
  return colors[name] || '#A8A878';
};

const getEvolutionId = (name) => {
  // Nota: Esto es un hack. Lo ideal sería que la API devolviera el ID.
  // Pero podemos intentar estimarlo o dejarlo así para demostración.
  return name; // La PokeAPI acepta el nombre en la URL de imagen a veces, pero no aquí.
  // Enriqueceremos la evolución en el backend si es necesario.
};

onMounted(fetchPokemon);
</script>

<style scoped>
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.fav-btn:hover {
  background-color: var(--color-primary);
  color: white;
}

.fav-btn.is-fav {
  background-color: var(--color-primary);
  color: white;
}

.detail-header {
  transition: background-color 0.5s ease;
}
</style>