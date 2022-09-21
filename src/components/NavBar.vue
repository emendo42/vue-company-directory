<script setup>
  import { ref } from 'vue'
  import { useAuth } from './composables/useAuth'

  const { isAuthenticated, logout, user } = useAuth()

  const brand = ref('🏫 Fake Company Directory 🏫')
</script>
<template>
  <nav>
    <div class="wrapper">
      <RouterLink :to="{ name: 'Home' }" class="brand">
        <span class="brand-title">{{ brand }}</span>
      </RouterLink>
      <div class="menu">
        
          <p v-show="isAuthenticated" class="px-1 py-6">
            Hello👋
            <strong
              ><i>{{ user.name }}</i></strong
            >
          </p>
          <div v-if="isAuthenticated">
          <RouterLink :to="{ name: 'Home' }" href="#" class="menu-item">Settings</RouterLink>
          <button :to="{ name: 'Home' }" href="#" class="menu-logout" @click="logout">Logout</button>
        </div>
        <div v-else>
          <RouterLink :to="{ name: 'Login' }" href="#" class="menu-login">Login</RouterLink>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped lang="postcss">
  nav {
    @apply flex h-20  bg-blue-900 text-slate-300;
    .wrapper {
      @apply container mx-auto flex w-full items-center justify-between;
      .brand {
        &-title {
          @apply text-2xl font-bold text-green-500;
        }
      }
      .menu {
        @apply flex gap-4;
        & div {
          @apply py-3;
        }
        &-item {
          @apply rounded-md px-4 py-3 hover:bg-green-500 hover:text-slate-900;
        }
        &-login {
          @apply rounded-md bg-green-200 px-4 py-3 font-bold text-slate-900 hover:bg-green-700 hover:text-slate-400;
        }
        &-logout {
          @apply mx-2 rounded-md bg-red-200 px-4 py-3 font-bold text-slate-900 hover:bg-red-700 hover:text-slate-400;
        }
      }
    }
  }
</style>
