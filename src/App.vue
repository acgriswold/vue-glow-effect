<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue';

import { useDark, useToggle } from '@vueuse/core';

const isDark = useDark();
const toggleDark = useToggle(isDark);
</script>

<template>
  <main class="bg-slate-50 dark:bg-slate-700 p-8">
    <div class="min-h-screen grid grid-cols-1 items-start">
      <button @click="toggleDark()" class="text-slate-700 dark:text-slate-50">
        toggle {{ isDark ? 'light' : 'dark' }}
      </button>

      <div class="flex flex-row self-stretch justify-center items-top">
        <a href="https://vitejs.dev" target="_blank">
          <img src="/vite.svg" class="logo" alt="Vite logo" />
        </a>
        <a href="https://vuejs.org/" target="_blank">
          <img src="/vue.svg" class="logo vue" alt="Vue logo" />
        </a>
      </div>
    </div>
  </main>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
