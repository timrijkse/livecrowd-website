<script setup lang="ts">
import SiteHeader from './components/SiteHeader.vue'
</script>

<template>
  <SiteHeader />

  <main class="main">
    <RouterView />
  </main>
</template>

<style scoped>
.main {
  width: 100%;
  max-width: var(--site-width);
  margin: 0 auto;
  padding: 0 var(--site-padding);
  padding-top: 100px;
}

@media (min-width: 1024px) {
  .main {
    /* padding-top: 300px; */
  }
}
</style>
