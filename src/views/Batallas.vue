<template>
  <div class="batallas-view">
    <header class="view-header" style="margin-bottom: 2rem;">
      <h1 style="font-size: 2.5rem; color: var(--color-primary); margin-bottom: 0.5rem;">Arena de Batalla</h1>
      <p style="color: #666;">Desafía a tus amigos y demuestra quién es el mejor entrenador.</p>
    </header>

    <div v-if="!inBattle" class="battle-setup" style="display: grid; grid-template-columns: 1fr 1fr; gap: 2rem;">
      <!-- Selección de Equipo -->
      <div style="background: white; padding: 2rem; border-radius: 20px; box-shadow: var(--shadow);">
        <h2 style="margin-bottom: 1.5rem; color: var(--color-accent);">1. Selecciona tu Equipo</h2>
        <div v-if="teams.length === 0" style="padding: 1rem; background: #fff5f5; border-radius: 12px; color: var(--color-primary); border: 1px solid #fee2e2;">
          <p>Debes crear un equipo en la sección <strong>Equipos</strong> antes de batallar.</p>
        </div>
        <div v-else style="display: flex; flex-direction: column; gap: 1rem;">
          <div v-for="team in teams" :key="team._id" @click="selectedTeam = team" 
               style="cursor: pointer; padding: 1rem; border-radius: 12px; border: 2px solid #eee; transition: all 0.3s;"
               :style="{ borderColor: selectedTeam?._id === team._id ? 'var(--color-primary)' : '#eee', background: selectedTeam?._id === team._id ? '#fff5f5' : 'white' }">
            <div style="font-weight: bold; margin-bottom: 0.5rem; text-transform: capitalize;">{{ team.name }}</div>
            <div style="display: flex; gap: 0.3rem;">
              <img v-for="p in team.pokemons" :key="p.pokemonId" :src="p.image" style="width: 30px; height: 30px;" />
            </div>
          </div>
        </div>
      </div>

      <!-- Selección de Rival -->
      <div style="background: white; padding: 2rem; border-radius: 20px; box-shadow: var(--shadow);">
        <h2 style="margin-bottom: 1.5rem; color: var(--color-accent);">2. Desafía a un Amigo</h2>
        <div v-if="friends.length === 0" style="padding: 1rem; background: #f9f9f9; border-radius: 12px; color: #666;">
          <p>No tienes amigos agregados. Ve a la sección <strong>Amigos</strong>.</p>
        </div>
        <div v-else style="display: flex; flex-direction: column; gap: 1rem;">
          <div v-for="friend in friends" :key="friend.id" @click="selectedFriend = friend" 
               style="cursor: pointer; padding: 1rem; border-radius: 12px; border: 2px solid #eee; transition: all 0.3s; display: flex; align-items: center; gap: 1rem;"
               :style="{ borderColor: selectedFriend?.id === friend.id ? 'var(--color-primary)' : '#eee', background: selectedFriend?.id === friend.id ? '#fff5f5' : 'white' }">
            <div style="width: 40px; height: 40px; background: var(--color-primary); border-radius: 50%; display: flex; align-items: center; justify-content: center; color: white;">{{ friend.username?.[0] }}</div>
            <div style="font-weight: bold;">{{ friend.username }}</div>
          </div>
        </div>

        <button @click="startBattle" :disabled="!selectedTeam || !selectedFriend" class="nav-link" style="width: 100%; margin-top: 2rem; border: none; cursor: pointer; text-align: center; padding: 1rem;" :style="{ opacity: (!selectedTeam || !selectedFriend) ? 0.5 : 1 }">
          ¡Comenzar Batalla! ⚔️
        </button>
      </div>
    </div>

    <!-- Arena de Batalla (Simulación) -->
    <div v-else class="battle-arena" style="background: #2a2a2a; border-radius: 20px; padding: 3rem; color: white; text-align: center; position: relative; overflow: hidden; min-height: 500px;">
      <div v-if="battleState === 'intro'" @click="battleState = 'ongoing'">
        <h1 style="font-size: 4rem; margin-bottom: 2rem; animation: pulse 1s infinite;">VS</h1>
        <div style="display: flex; justify-content: space-around; align-items: center;">
          <div class="player-intro">
            <h2 style="color: var(--color-primary);">Tú</h2>
            <img :src="selectedTeam.pokemons[0].image" style="width: 200px; height: 200px;" />
            <h3>{{ selectedTeam.pokemons[0].pokemonName }}</h3>
          </div>
          <div class="rival-intro">
            <h2 style="color: #6890F0;">{{ selectedFriend.username }}</h2>
            <div style="width: 200px; height: 200px; background: rgba(255,255,255,0.1); border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: auto;">
              <span style="font-size: 5rem;">?</span>
            </div>
            <h3>Oponente</h3>
          </div>
        </div>
        <p style="margin-top: 3rem; opacity: 0.7;">Haz clic para continuar...</p>
      </div>

      <div v-if="battleState === 'ongoing'">
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 3rem;">
           <!-- Rival -->
           <div style="text-align: right;">
             <div style="background: white; color: black; padding: 1rem; border-radius: 10px; width: 250px; text-align: left;">
               <div style="font-weight: bold;">Rival</div>
               <div style="height: 10px; background: #eee; border-radius: 5px; margin-top: 0.5rem; overflow: hidden;">
                 <div :style="{ width: `${rivalHP}%` }" style="height: 100%; background: #4caf50; transition: width 0.5s;"></div>
               </div>
             </div>
             <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" style="width: 150px; transform: scaleX(-1);" />
           </div>

           <!-- Tú -->
           <div style="text-align: left;">
             <img :src="selectedTeam.pokemons[0].image" style="width: 180px;" />
             <div style="background: white; color: black; padding: 1rem; border-radius: 10px; width: 250px;">
               <div style="font-weight: bold;">{{ selectedTeam.pokemons[0].pokemonName }}</div>
               <div style="height: 10px; background: #eee; border-radius: 5px; margin-top: 0.5rem; overflow: hidden;">
                 <div :style="{ width: `${myHP}%` }" style="height: 100%; background: #4caf50; transition: width 0.5s;"></div>
               </div>
             </div>
           </div>
        </div>

        <!-- Acciones -->
        <div class="actions" style="background: rgba(0,0,0,0.5); padding: 2rem; border-radius: 15px; display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;">
          <button @click="attack" :disabled="isAttacking" class="action-btn">Atacar ⚔️</button>
          <button @click="battleState = 'result'" class="action-btn" style="background: #555;">Huir 🏃</button>
          <div style="grid-column: span 2; padding-top: 1rem; min-height: 50px; color: #aaa;">{{ battleMsg }}</div>
        </div>
      </div>

      <div v-if="battleState === 'result'" style="padding-top: 5rem;">
        <h1 style="font-size: 5rem; margin-bottom: 1rem;">{{ rivalHP <= 0 ? '¡VICTORIA!' : 'DERROTA' }}</h1>
        <p style="font-size: 1.5rem; margin-bottom: 3rem;">{{ rivalHP <= 0 ? 'Has ganado la batalla' : 'Has sido derrotado' }}</p>
        <button @click="resetBattle" class="nav-link" style="border: none; cursor: pointer; padding: 1rem 2rem;">Volver a la Arena</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import api from '../services/api';

const teams = ref([]);
const friends = ref([]);
const selectedTeam = ref(null);
const selectedFriend = ref(null);
const inBattle = ref(false);
const battleState = ref('intro'); // intro, ongoing, result
const myHP = ref(100);
const rivalHP = ref(100);
const battleMsg = ref('¡Es tu turno!');
const isAttacking = ref(false);

const fetchTeams = async () => {
  const res = await api.get('/teams');
  teams.value = res.data.teams;
};

const fetchFriends = async () => {
  const res = await api.get('/friends');
  friends.value = res.data.friends;
};

const startBattle = () => {
  inBattle.value = true;
  battleState.value = 'intro';
  myHP.value = 100;
  rivalHP.value = 100;
};

const attack = () => {
  if (isAttacking.value) return;
  isAttacking.value = true;
  
  // Tu ataque
  const damage = Math.floor(Math.random() * 20) + 10;
  rivalHP.value = Math.max(0, rivalHP.value - damage);
  battleMsg.value = `¡Tu ${selectedTeam.value.pokemons[0].pokemonName} causó ${damage} de daño!`;

  if (rivalHP.value <= 0) {
    setTimeout(() => battleState.value = 'result', 1000);
    return;
  }

  // Contraataque
  setTimeout(() => {
    const rivalDamage = Math.floor(Math.random() * 15) + 5;
    myHP.value = Math.max(0, myHP.value - rivalDamage);
    battleMsg.value = `¡El rival contraatacó por ${rivalDamage}!`;
    
    if (myHP.value <= 0) {
      setTimeout(() => battleState.value = 'result', 1000);
    }
    isAttacking.value = false;
  }, 1000);
};

const resetBattle = () => {
  inBattle.value = false;
  selectedTeam.value = null;
  selectedFriend.value = null;
};

onMounted(() => {
  fetchTeams();
  fetchFriends();
});
</script>

<style scoped>
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.1); }
  100% { transform: scale(1); }
}

.action-btn {
  padding: 1rem;
  font-size: 1.2rem;
  font-weight: bold;
  border: none;
  border-radius: 10px;
  background: var(--color-primary);
  color: white;
  cursor: pointer;
  transition: all 0.2s;
}

.action-btn:hover:not(:disabled) {
  transform: scale(1.02);
  filter: brightness(1.1);
}

.action-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>