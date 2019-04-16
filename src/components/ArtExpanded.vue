<template>
  <div class='ArtExpanded'>
    <div class='info-flex'>
      <p class='date'><span class='info-head'>Date:</span> {{this.date}}</p>
      <span class='info-head bullet'>❊</span>
      <p class='image-id'><span class='info-head'>Harvard Image Id:</span> {{this.imageid}}</p>
    </div>
    <div class='button-flex'>
      <div class='navbutton'@click="$emit('close')">
        <p class='buttontext'>← Go Back</p>
      </div>
      <div class='navbutton'>
        <a class='buttontext' target='_blank' :href='`${this.imageUrl}`'>Full Resolution</a>
      </div>
    </div>
    <img v-bind:src='`${this.imageUrl}`' class='fullimage'/>
    <p class='copyright'>All images are copyright President and Fellows of Harvard College.</p>
  </div>
</template>

<script>
import Vue from 'vue';

Vue.component('modal', {
  template: '#modal-template'
})

export default {
  name: 'ArtExpanded',
  props: ['imageUrl', 'date', 'imageid']
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
  .button-flex {
    display: flex;
    justify-content: space-around;
    width: 100%;
  }
  .info-head {
    font-size: 30px;
    padding: 0px 20px;
  }
  .image-id {
    padding-right: 8px;
  }
  .navbutton {
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
  .buttontext {
    text-decoration: none;
    color: black;
    font-size: 26px;
  }
  .copyright {
    font-size: 20px;
    font-family: Seaweed Script;
    margin: 10px 2px;
    color: #6b5565;
  }
  .navbutton:hover {
    cursor: pointer;
    background-color: #c7ccdd;
  }
  .navbutton:hover a,
  .navbutton:hover p {
    color: white;
    text-shadow: 1px 1px black;
  }
</style>
