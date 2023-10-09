<script setup>
import SearchBar from './components/SearchBar.vue';
import Map from './components/Map.vue';
</script>

<template>
  <div style="text-align: center;">
    <header>
      <Map/>
      <SearchBar />
    </header>
  </div>
      </template>

<style scoped>

header {
  position: absolute;
  top: 0;
  right: 0;
  width: 100%;
  height: 100%;
  line-height: 1.5;
}
</style>
