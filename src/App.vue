<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue';

import { useDark, useToggle, useMouse } from '@vueuse/core';
import { computed, HTMLElement, ref } from 'vue';

const isDark = useDark();
const toggleDark = useToggle(isDark);

const { x, y } = useMouse();


const spotlit = ref<HTMLElement>
const spotlightGradient = computed(
  () => {
    let rect = spotlit.value?.getBoundingClientRect()
    const xPos = x.value - (rect?.left ?? 0)
    const yPos = y.value - (rect?.top ?? 0)
    return `radial-gradient(circle at ${xPos}px ${yPos}px, black 15%, transparent 50%)`
  }

);
</script>

<template>
  <main
    class="
      relative
      min-h-screen
      p-8
      flex flex-col
      bg-slate-50
      dark:bg-slate-700
      bg-gradient-to-b
      from-slate-50
      to-green-500/30
      dark:from-slate-700 dark:to-green-500/30
      from-60%
      overflow-hidden
    "
  >
    <div
      class="
        absolute
        bg-green-500/30
        rounded-full
        -translate-x-1/2 -translate-y-1/2
        blur-3xl
        pointer-events-none
      "
      :style="{
        left: `${x}px`,
        top: `${y}px`,
        width: `200px`,
        height: `200px`,
      }"
    ></div>

    <button @click="toggleDark()" class="text-slate-700 dark:text-slate-50">
      toggle {{ isDark ? 'light' : 'dark' }}
    </button>

    <div
      class="flex-1 flex flex-row justify-center items-center"
      ref="spotlit"
      :style="{ maskImage: spotlightGradient }"
    >
      <a href="https://vitejs.dev" target="_blank">
        <img src="/vite.svg" class="logo" alt="Vite logo" />
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="/vue.svg" class="logo vue" alt="Vue logo" />
      </a>
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
