<template>
  <div class='ArtExpanded'>
    <div class='info-flex'>
      <p class='date'><span class='info-head'>Date:</span> {{this.date}}</p>
      <span class='info-head bullet'>❊</span>
      <p class='image-id'><span class='info-head'>Harvard Image Id:</span> {{this.imageid}}</p>
    </div>
    <div class='viewlink-button'>
      <a class='viewlink' target='_blank' :href='`${this.imageUrl}`'>Full Resolution</a>
    </div>
    <img v-bind:src='`${this.imageUrl}`' class='fullimage'/>
    <p class='copyright'>All images are copyright President and Fellows of Harvard College.</p>
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
  p, span {
    margin: 0;
    padding: 0;
  }
  .ArtExpanded {
    position: fixed;
    z-index: 100;
    top: 20%;
    right: 34%;
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    border: 6px solid #A0DED7;
    border-radius: 15px;
  }
  .fullimage {
    max-height: 475px;
    max-width: 475px;
    border: 4px solid #6b5565;
  }
  .info-flex {
    display: flex;
    justify-content: space-around;
    width: 100%;
    font-size: 24px;
    margin: 10px 1px;
  }
  .info-head {
    font-size: 30px;
    padding: 0px 20px;
  }
  .image-id {
    padding-right: 8px;
  }
  .viewlink-button {
    padding: 5px 20px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 4px solid #D4A3C8;
    border-radius: 12px;
    background-color: white;
    margin-bottom: 10px;
  }
  .bullet {
    padding: 0px;
    padding-left: 20px;
    font-size: 30px;
  }
  .viewlink {
    text-decoration: none;
    color: black;
    font-size: 26px;
  }
  .copyright {
    font-size: 20px;
    font-family: Seaweed Script;
    margin: 10px 2px;
  }
  .viewlink-button:hover {
    cursor: pointer;
    background-color: #c7ccdd;
  }
  .viewlink-button:hover a {
    color: white;
    text-shadow: 1px 1px black;
  }
</style>
