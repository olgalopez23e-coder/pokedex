<template>
  <div class="batallas-view">
<<<<<<< HEAD
    <header class="view-header">
      <h1>Arena de Batalla</h1>
      <p class="subtitle">Desafía a tus amigos y demuestra quién es el mejor entrenador.</p>
    </header>

    <div v-if="!inBattle" class="battle-setup">
      <!-- Selección de Equipo -->
      <div class="setup-card">
        <h2>1. Selecciona tu Equipo</h2>
        <div v-if="teams.length === 0" class="empty-state warning">
          <p>Debes crear un equipo en la sección <strong>Equipos</strong> antes de batallar.</p>
        </div>
        <div v-else class="option-list">
          <div
            v-for="team in teams"
            :key="team._id"
            @click="selectedTeam = team"
            class="option-card"
            :class="{ selected: selectedTeam?._id === team._id }"
          >
            <div class="option-title">{{ team.name }}</div>
            <div class="team-pokemons">
              <img v-for="p in team.pokemons" :key="p.pokemonId" :src="p.image" class="mini-pokemon" />
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
            </div>
          </div>
        </div>
      </div>

      <!-- Selección de Rival -->
<<<<<<< HEAD
      <div class="setup-card">
        <h2>2. Desafía a un Amigo</h2>
        <div v-if="friends.length === 0" class="empty-state neutral">
          <p>No tienes amigos agregados. Ve a la sección <strong>Amigos</strong>.</p>
        </div>
        <div v-else class="option-list">
          <div
            v-for="friend in friends"
            :key="friend.id"
            @click="selectedFriend = friend"
            class="option-card friend-card"
            :class="{ selected: selectedFriend?.id === friend.id }"
          >
            <div class="friend-avatar">{{ friend.username?.[0] }}</div>
            <div class="option-title">{{ friend.username }}</div>
          </div>
        </div>

        <button @click="startBattle" :disabled="!selectedTeam || !selectedFriend" class="start-btn">
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
          ¡Comenzar Batalla! ⚔️
        </button>
      </div>
    </div>

    <!-- Arena de Batalla (Simulación) -->
<<<<<<< HEAD
    <div v-else class="battle-arena">
      <div v-if="battleState === 'intro'" @click="battleState = 'ongoing'">
        <h1 class="vs-title">VS</h1>
        <div class="battle-intro-grid">
          <div class="player-intro">
            <h2 class="player-name">Tú</h2>
            <img :src="selectedTeam.pokemons[0].image" class="intro-pokemon" />
            <h3>{{ selectedTeam.pokemons[0].pokemonName }}</h3>
          </div>
          <div class="rival-intro">
            <h2 class="rival-name">{{ selectedFriend.username }}</h2>
            <div class="rival-circle">
              <span class="rival-mark">?</span>
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
            </div>
            <h3>Oponente</h3>
          </div>
        </div>
<<<<<<< HEAD
        <p class="hint">Haz clic para continuar...</p>
      </div>

      <div v-if="battleState === 'ongoing'">
        <div class="battle-layout">
           <!-- Rival -->
           <div class="battler rival">
             <div class="hp-card">
               <div class="hp-name">Rival</div>
               <div class="hp-track">
                 <div :style="{ width: `${rivalHP}%` }" class="hp-fill"></div>
               </div>
             </div>
             <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png" class="rival-sprite" />
           </div>

           <!-- Tú -->
           <div class="battler player">
             <img :src="selectedTeam.pokemons[0].image" class="player-sprite" />
             <div class="hp-card">
               <div class="hp-name">{{ selectedTeam.pokemons[0].pokemonName }}</div>
               <div class="hp-track">
                 <div :style="{ width: `${myHP}%` }" class="hp-fill"></div>
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
               </div>
             </div>
           </div>
        </div>

        <!-- Acciones -->
<<<<<<< HEAD
        <div class="actions">
          <button @click="attack" :disabled="isAttacking" class="action-btn">Atacar ⚔️</button>
          <button @click="battleState = 'result'" class="action-btn escape-btn">Huir 🏃</button>
          <div class="battle-msg">{{ battleMsg }}</div>
        </div>
      </div>

      <div v-if="battleState === 'result'" class="result-screen">
        <h1>{{ rivalHP <= 0 ? '¡VICTORIA!' : 'DERROTA' }}</h1>
        <p>{{ rivalHP <= 0 ? 'Has ganado la batalla' : 'Has sido derrotado' }}</p>
        <button @click="resetBattle" class="start-btn back-btn">Volver a la Arena</button>
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
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
<<<<<<< HEAD
.batallas-view {
  padding: 0.25rem;
}

.view-header {
  margin-bottom: 2rem;
}

.view-header h1 {
  margin: 0;
  font-size: 2.4rem;
  color: #d90429;
  letter-spacing: 0.2px;
}

.subtitle {
  margin-top: 0.5rem;
  color: #495057;
}

.battle-setup {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.setup-card {
  background: linear-gradient(170deg, #ffffff 0%, #f8fbff 100%);
  padding: 1.5rem;
  border-radius: 18px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
  border: 1px solid #edf2f7;
}

.setup-card h2 {
  margin-bottom: 1rem;
  color: #213547;
}

.empty-state {
  padding: 1rem;
  border-radius: 12px;
}

.empty-state.warning {
  background: #fff2f2;
  color: #c1121f;
  border: 1px solid #ffd4d9;
}

.empty-state.neutral {
  background: #f5f7fa;
  color: #52606d;
}

.option-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.option-card {
  cursor: pointer;
  padding: 0.9rem;
  border-radius: 12px;
  border: 2px solid #e9eef5;
  background: #fff;
  transition: transform 0.15s ease, border-color 0.2s ease, box-shadow 0.2s ease;
}

.option-card:hover {
  transform: translateY(-2px);
  border-color: #b9d6ff;
  box-shadow: 0 8px 18px rgba(25, 118, 210, 0.12);
}

.option-card.selected {
  border-color: #d90429;
  background: #fff3f5;
}

.option-title {
  font-weight: 700;
  text-transform: capitalize;
}

.friend-card {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.friend-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  color: #fff;
  font-weight: 700;
  background: linear-gradient(145deg, #d90429 0%, #ef476f 100%);
}

.team-pokemons {
  display: flex;
  gap: 0.3rem;
  margin-top: 0.4rem;
}

.mini-pokemon {
  width: 32px;
  height: 32px;
}

.start-btn {
  width: 100%;
  margin-top: 1.25rem;
  border: none;
  cursor: pointer;
  text-align: center;
  padding: 0.9rem;
  border-radius: 12px;
  color: #fff;
  font-weight: 700;
  background: linear-gradient(135deg, #d90429 0%, #ef233c 100%);
  transition: transform 0.2s ease, filter 0.2s ease, opacity 0.2s ease;
}

.start-btn:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}

.start-btn:hover:not(:disabled) {
  transform: translateY(-1px);
  filter: brightness(1.05);
}

.battle-arena {
  background: radial-gradient(circle at 20% 20%, #243b55 0%, #141e30 50%, #0b1220 100%);
  border-radius: 20px;
  padding: 2rem;
  color: white;
  text-align: center;
  position: relative;
  overflow: hidden;
  min-height: 500px;
}

.vs-title {
  font-size: 4rem;
  margin-bottom: 2rem;
  animation: pulse 1s infinite;
}

.battle-intro-grid {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.player-name {
  color: #ffd166;
}

.rival-name {
  color: #8ecae6;
}

.intro-pokemon {
  width: 180px;
  height: 180px;
}

.rival-circle {
  width: 180px;
  height: 180px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  display: grid;
  place-items: center;
  margin: auto;
}

.rival-mark {
  font-size: 4.5rem;
}

.hint {
  margin-top: 2rem;
  opacity: 0.8;
}

.battle-layout {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2.5rem;
}

.battler {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.battler.rival {
  align-items: flex-end;
}

.battler.player {
  align-items: flex-start;
}

.hp-card {
  background: #ffffff;
  color: #101828;
  padding: 0.85rem;
  border-radius: 10px;
  width: 250px;
  text-align: left;
}

.hp-name {
  font-weight: 700;
  text-transform: capitalize;
}

.hp-track {
  height: 10px;
  background: #e6e9ef;
  border-radius: 8px;
  margin-top: 0.5rem;
  overflow: hidden;
}

.hp-fill {
  height: 100%;
  background: linear-gradient(90deg, #2ecc71 0%, #5be584 100%);
  transition: width 0.5s;
}

.rival-sprite {
  width: 150px;
  transform: scaleX(-1);
}

.player-sprite {
  width: 180px;
}

.actions {
  background: rgba(0, 0, 0, 0.35);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 1.4rem;
  border-radius: 15px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.9rem;
}

=======
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.1); }
  100% { transform: scale(1); }
}

.action-btn {
  padding: 1rem;
<<<<<<< HEAD
  font-size: 1rem;
  font-weight: bold;
  border: none;
  border-radius: 10px;
  background: linear-gradient(135deg, #d90429 0%, #ef233c 100%);
  color: white;
  cursor: pointer;
  transition: transform 0.2s ease, filter 0.2s ease;
}

.action-btn:hover:not(:disabled) {
  transform: translateY(-1px);
  filter: brightness(1.06);
=======
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
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
}

.action-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
<<<<<<< HEAD

.escape-btn {
  background: linear-gradient(135deg, #475569 0%, #334155 100%);
}

.battle-msg {
  grid-column: span 2;
  padding-top: 0.5rem;
  min-height: 44px;
  color: #dbe8ff;
}

.result-screen {
  padding-top: 4.5rem;
}

.result-screen h1 {
  font-size: 4rem;
  margin-bottom: 0.5rem;
}

.result-screen p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

.back-btn {
  max-width: 260px;
  margin: 0 auto;
}

@media (max-width: 900px) {
  .battle-setup {
    grid-template-columns: 1fr;
  }

  .battle-layout {
    flex-direction: column;
    gap: 1.2rem;
  }

  .battler.rival,
  .battler.player {
    align-items: center;
  }

  .battle-intro-grid {
    flex-direction: column;
    gap: 1.25rem;
  }

  .actions {
    grid-template-columns: 1fr;
  }

  .battle-msg {
    grid-column: span 1;
  }
}
=======
>>>>>>> 5ac1609e264fd44ad0d1ccdf2f3ad0075d804495
</style>