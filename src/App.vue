<script setup lang="ts">
import Header from './components/header/Header.vue'
import Content from './components/content/Content.vue'
</script>

<template>
  <div class="mx-auto lg:py-0 py-12 lg:px-24 md:px-16 px-8 max-w-screen-xl min-h-screen">
    <div class="lg:flex lg:gap-4 lg:justify-between">
      <Header/>
      <Content/>
    </div>
  </div>
</template>

<style scoped>
</style>
