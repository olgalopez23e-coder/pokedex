<template>
<<<<<<< HEAD
  <div v-if="loading" class="loading-state">
    <div class="loader"></div>
    <p>Buscando datos del Pokémon...</p>
  </div>

  <div v-else-if="pokemon" class="pokemon-detail">
    <div class="detail-container">
      
      <!-- Lado Izquierdo: Imagen y Tipos -->
      <div class="detail-header" :class="`bg-${pokemon.types[0]}`">
        <button @click="$router.back()" class="back-btn">← Volver</button>
        
        <img :src="pokemon.image" :alt="pokemon.name" class="hero-image" />
        <h1 class="hero-name">{{ pokemon.name }}</h1>
        <div class="pokemon-types hero-types">
          <span v-for="type in pokemon.types" :key="type" :class="['type-badge', `type-${type}`]" class="hero-type-badge">
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
            {{ type }}
          </span>
        </div>
      </div>

      <!-- Lado Derecho: Info y Stats -->
<<<<<<< HEAD
      <div class="detail-body">
        <div class="detail-top">
          <div>
            <h2 class="section-title">Descripción</h2>
            <p class="description">{{ pokemon.description }}</p>
          </div>
          <button @click="toggleFavorito" :class="['fav-btn', { 'is-fav': esFavorito }]">
            <span class="heart-icon">{{ esFavorito ? '❤️' : '🤍' }}</span>
=======
      <div class="detail-body" style="padding: 2.5rem;">
        <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 2rem;">
          <div>
            <h2 style="color: var(--color-primary); margin-bottom: 0.5rem;">Descripción</h2>
            <p style="font-size: 1.1rem; color: #444; max-width: 600px;">{{ pokemon.description }}</p>
          </div>
          <button @click="toggleFavorito" :class="['fav-btn', { 'is-fav': esFavorito }]" style="padding: 1rem 1.5rem; border-radius: 12px; border: 2px solid var(--color-primary); cursor: pointer; transition: all 0.3s ease; font-weight: bold; display: flex; align-items: center; gap: 0.5rem;">
            <span style="font-size: 1.5rem;">{{ esFavorito ? '❤️' : '🤍' }}</span>
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
            {{ esFavorito ? 'En Favoritos' : 'Añadir a Favoritos' }}
          </button>
        </div>

<<<<<<< HEAD
        <div class="detail-grid">
          <!-- Datos Básicos -->
          <div>
            <h3 class="subsection-title">Datos</h3>
            <div class="data-list">
              <div class="data-row"><span>Altura:</span> <strong>{{ pokemon.height / 10 }} m</strong></div>
              <div class="data-row"><span>Peso:</span> <strong>{{ pokemon.weight / 10 }} kg</strong></div>
              <div class="data-row"><span>Especie:</span> <strong class="capitalize">{{ pokemon.species }}</strong></div>
              <div class="data-row"><span>Habilidades:</span> 
                <div class="abilities-list">
                  <div v-for="a in pokemon.abilities" :key="a.name" class="capitalize">{{ a.name }} {{ a.isHidden ? '(oculta)' : '' }}</div>
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
                </div>
              </div>
            </div>
          </div>

          <!-- Estadísticas -->
          <div>
<<<<<<< HEAD
            <h3 class="subsection-title">Estadísticas Base</h3>
            <div v-for="stat in pokemon.stats" :key="stat.name" class="stat-item">
              <div class="stat-head">
                <span class="stat-label">{{ stat.name }}</span>
                <strong>{{ stat.value }}</strong>
              </div>
              <div class="stat-track">
                <div :style="{ width: `${(stat.value / 255) * 100}%`, backgroundColor: getStatColor(stat.name) }" class="stat-fill"></div>
=======
            <h3 style="margin-bottom: 1rem; border-bottom: 2px solid #eee; padding-bottom: 0.5rem;">Estadísticas Base</h3>
            <div v-for="stat in pokemon.stats" :key="stat.name" style="margin-bottom: 1rem;">
              <div style="display: flex; justify-content: space-between; margin-bottom: 0.3rem;">
                <span style="text-transform: uppercase; font-size: 0.8rem; font-weight: bold; color: #666;">{{ stat.name }}</span>
                <strong>{{ stat.value }}</strong>
              </div>
              <div style="height: 10px; background: #eee; border-radius: 5px; overflow: hidden;">
                <div :style="{ width: `${(stat.value / 255) * 100}%`, backgroundColor: getStatColor(stat.name) }" style="height: 100%; transition: width 1s ease-out;"></div>
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
              </div>
            </div>
          </div>
        </div>

        <!-- Línea Evolutiva -->
<<<<<<< HEAD
        <div v-if="pokemon.evolutionChain && pokemon.evolutionChain.length > 1" class="evolution-section">
          <h3 class="subsection-title">Línea Evolutiva</h3>
          <div class="evolution-row">
            <template v-for="(name, index) in pokemon.evolutionChain" :key="name">
              <div class="evolution-node" @click="$router.push(`/pokemon/${name}`)">
                <div class="evolution-img-wrap" onmouseover="this.style.borderColor='var(--color-primary)'" onmouseout="this.style.borderColor='transparent'">
                  <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getEvolutionId(name)}.png`" class="evolution-img" />
                </div>
                <div class="evolution-name">{{ name }}</div>
              </div>
              <span v-if="index < pokemon.evolutionChain.length - 1" class="evolution-arrow">➜</span>
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
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

<<<<<<< HEAD
.loading-state {
  text-align: center;
  padding: 5rem;
}

.loader {
  width: 60px;
  height: 60px;
  border: 6px solid #2a344b;
  border-top: 6px solid var(--color-primary);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: auto;
}

.loading-state p {
  margin-top: 1.5rem;
  font-size: 1.1rem;
  color: var(--color-text-muted);
}

.detail-container {
  background: linear-gradient(170deg, #161d2d 0%, #111827 100%);
  border: 1px solid var(--color-border);
  border-radius: 20px;
  box-shadow: var(--shadow);
  overflow: hidden;
  display: grid;
  grid-template-columns: 1fr 1.4fr;
}

.detail-header {
  padding: 2.4rem;
  text-align: center;
  color: white;
  background-color: var(--color-primary);
  position: relative;
}

.back-btn {
  position: absolute;
  top: 1rem;
  left: 1rem;
  background: rgba(0, 0, 0, 0.22);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  padding: 0.45rem 0.85rem;
  border-radius: 20px;
  cursor: pointer;
}

.hero-image {
  width: 220px;
  height: 220px;
  filter: drop-shadow(0 12px 22px rgba(0, 0, 0, 0.34));
}

.hero-name {
  text-transform: capitalize;
  font-size: 2.3rem;
  margin-top: 0.8rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.hero-types {
  justify-content: center;
  margin-top: 1rem;
  gap: 0.6rem;
}

.hero-type-badge {
  font-size: 0.9rem;
  padding: 0.45rem 1rem;
}

.detail-body {
  padding: 2.1rem;
}

.detail-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.6rem;
}

.section-title {
  color: var(--color-primary);
  margin-bottom: 0.6rem;
}

.description {
  font-size: 1.05rem;
  color: var(--color-text);
  max-width: 600px;
}

.fav-btn {
  padding: 0.85rem 1.1rem;
  border-radius: 12px;
  border: 2px solid var(--color-primary);
  background: rgba(225, 29, 47, 0.08);
  color: var(--color-text);
  cursor: pointer;
  transition: all 0.25s ease;
  font-weight: bold;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  white-space: nowrap;
}

.heart-icon {
  font-size: 1.3rem;
}

.detail-grid {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 2rem;
}

.subsection-title {
  margin-bottom: 1rem;
  border-bottom: 2px solid #2a344b;
  padding-bottom: 0.5rem;
  color: var(--color-text);
}

.data-list {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.data-row {
  display: flex;
  justify-content: space-between;
  gap: 0.6rem;
}

.data-row span {
  color: var(--color-text-muted);
}

.data-row strong {
  color: var(--color-text);
}

.abilities-list {
  text-align: right;
  color: var(--color-text);
}

.capitalize {
  text-transform: capitalize;
}

.stat-item {
  margin-bottom: 1rem;
}

.stat-head {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.3rem;
}

.stat-head strong {
  color: var(--color-text);
}

.stat-label {
  text-transform: uppercase;
  font-size: 0.78rem;
  font-weight: bold;
  color: var(--color-text-muted);
}

.stat-track {
  height: 10px;
  background: #2a344b;
  border-radius: 5px;
  overflow: hidden;
}

.stat-fill {
  height: 100%;
  transition: width 1s ease-out;
}

.evolution-section {
  margin-top: 2.2rem;
}

.evolution-row {
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 0.8rem;
  flex-wrap: wrap;
}

.evolution-node {
  text-align: center;
  cursor: pointer;
}

.evolution-img-wrap {
  width: 80px;
  height: 80px;
  background: #0f1422;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.5rem;
  border: 2px solid transparent;
  transition: all 0.3s;
}

.evolution-img {
  width: 60px;
  height: 60px;
}

.evolution-name {
  text-transform: capitalize;
  font-weight: bold;
  font-size: 0.9rem;
  color: var(--color-text);
}

.evolution-arrow {
  font-size: 1.4rem;
  color: #6f7f9f;
}

=======
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
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
<<<<<<< HEAD

@media (max-width: 980px) {
  .detail-container {
    grid-template-columns: 1fr;
  }

  .hero-name {
    font-size: 1.9rem;
  }

  .detail-top {
    flex-direction: column;
    align-items: stretch;
  }

  .fav-btn {
    width: 100%;
    justify-content: center;
  }

  .detail-grid {
    grid-template-columns: 1fr;
  }
}
=======
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
</style>