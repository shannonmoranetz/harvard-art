<template>
  <div id="app">
    <ArtSection />
  </div>
</template>

<script>
import ArtSection from './components/ArtSection.vue'

export default {
  name: 'app',
  components: {
    ArtSection
  }
}
</script>

<style>
#app {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
</style>
