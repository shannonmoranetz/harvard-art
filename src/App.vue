<template>
  <div id="app">
    <ArtSection />
  </div>
</template>

<script>
import Vue from 'vue'
import ArtSection from './components/ArtSection.vue'

export default {
  name: 'app',
  components: {
    ArtSection
  }
}
</script>

<style>
html {
  min-height: 100%;
  background: linear-gradient(to bottom, #fcecfc 0%, #81ead5 20%, #fba6e1 40%, #bae5ef 60%, #e3eabe 80%, #f2c09b 100%);
  background-repeat: no-repeat;
  background-size: cover;
}
#app {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
</style>
