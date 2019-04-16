<template>
  <div class='ArtExpanded'>
    <img v-bind:src='`${this.imageUrl}`'></img>
  </div>
</template>

<script>

export default {
  name: 'ArtExpanded',
  props: ['imageUrl'],
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
  }
</style>
