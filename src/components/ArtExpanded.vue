<template>
  <div class='ArtExpanded'>
    <p class='date'>{{this.date}}</p>
    <p class='image-id'>{{this.imageid}}</p>
    <img v-bind:src='`${this.imageUrl}`' class='fullimage'/>
  </div>
</template>

<script>

export default {
  name: 'ArtExpanded',
  props: ['imageUrl', 'date', 'imageid'],
  methods: {
  }
}

</script>

<style scoped>
  .ArtExpanded {
    position: absolute;
    z-index: 100;
    top: 20%;
    right: 20%;
    background-color: white;
  }
  .fullimage {
    max-height: 800px;
    max-width: 800px;
  }
</style>
