<template>
  <header>
    <div class="flex mt-5 w-full justify-center gap-1">
      <nav class="flex gap-x-4 mb-4">
        <NavigationButton>
          <RouterLink to="/">Home</RouterLink>
        </NavigationButton>
        <NavigationButton>
          <RouterLink to="/about">About</RouterLink>
        </NavigationButton>
        <NavigationButton>
          <RouterLink to="/weather">Weather</RouterLink>
        </NavigationButton>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
import NavigationButton from './components/NavigationButton.vue'
</script>
