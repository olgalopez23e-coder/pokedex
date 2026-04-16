<template>
  <div id="app">
    <nav class="navbar">
      <div class="navbar-brand">
        <router-link to="/" class="nav-link" style="font-size: 1.5rem; display: flex; align-items: center; gap: 0.5rem;">
          <span>🔴</span> PokéPWA
        </router-link>
      </div>
      <div class="navbar-links">
        <router-link to="/" class="nav-link">Explorar</router-link>
        
        <template v-if="isLoggedIn">
          <router-link to="/favoritos" class="nav-link">Favoritos</router-link>
          <router-link to="/equipos" class="nav-link">Equipos</router-link>
          <router-link to="/amigos" class="nav-link">Amigos</router-link>
          <router-link to="/batallas" class="nav-link">Batallas</router-link>
          <button @click="handleLogout" class="nav-link logout-btn" style="background: none; border: 1px solid rgba(255,255,255,0.3); cursor: pointer;">
            Salir
          </button>
        </template>
        
        <template v-else>
          <router-link to="/login" class="nav-link">Entrar</router-link>
          <router-link to="/register" class="nav-link register-btn" style="background: var(--color-white); color: var(--color-primary);">
            Unirse
          </router-link>
        </template>
      </div>
    </nav>

    <main class="container">
      <router-view />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRouter } from 'vue-router';
import { requestNotificationPermission } from './services/notifications';

const router = useRouter();
const isLoggedIn = ref(!!localStorage.getItem('token'));

const updateAuth = () => {
  isLoggedIn.value = !!localStorage.getItem('token');
};

const handleLogout = () => {
  localStorage.removeItem('token');
  localStorage.removeItem('user');
  updateAuth();
  router.push('/login');
};

onMounted(async () => {
  window.addEventListener('auth-change', updateAuth);
  
  const granted = await requestNotificationPermission();
  if (granted) {
    console.log('Permiso de notificaciones concedido');
  }
});

onUnmounted(() => {
  window.removeEventListener('auth-change', updateAuth);
});
</script>

<style>
/* Los estilos globales ya están en style.css */
.logout-btn:hover {
  background-color: rgba(255,255,255,0.1) !important;
}

.register-btn:hover {
  background-color: #eee !important;
  color: var(--color-primary) !important;
}
</style>