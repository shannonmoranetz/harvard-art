<template>
  <div class='ArtExpanded'>
    <div class='info-flex'>
      <p class='date'><span class='info-head'>Date:</span> {{this.date}}</p>
      <p class='image-id'><span class='info-head'>Harvard Image Id:</span> {{this.imageid}}</p>
      <div class='viewlink-button'>
        <a class='viewlink' target='_blank' :href='`${this.imageUrl}`'>View Full Resolution</a>
      </div>
    </div>
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
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
  }
  .fullimage {
    max-height: 600px;
    max-width: 700px;
  }
  .info-flex {
    display: flex;
    justify-content: space-between;
    width: 100%;
  }
  .info-head {
    font-weight: bold;
    padding: 0px 10px;
  }
  .viewlink-button {
    padding: 4px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1px solid black;
  }
  .viewlink {
    text-decoration: none;
  }
</style>
