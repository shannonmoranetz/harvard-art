<template>
  <div class='ArtSection'>
    <header class='header'>
      <h1 class='artsection-title'>Harvard Art Museum</h1>
      <h2 class='subtitle'>Enjoy a random selection of Harvard's finest artwork.</h2>
      <div class='generate' v-on:click='fetchArt()'>
        <p class='generate-text'>New art, please!</p>
      </div>
    </header>
    <ul class='art-list'>
      <li v-if='artworks.length' v-for='artwork in artworks' :key='artwork.id' class='art-listitem'>
        <img :src='artwork.baseimageurl'
             :imageid='artwork.imageid'
             :date='artwork.date'
             v-on:click='expandImage()'
             class='artwork'
        />
      </li>
    </ul>
  <div v-if='!artworks.length' class='loading'>
    <h2 class='loading-text'>Loading...</h2>
  </div>
  <div v-bind:class="{'active':(isExpanded === true)}"></div>
  <ArtExpanded v-if='isExpanded' :imageUrl='this.imageUrl' :date='this.date' :imageid='this.imageid'/>
</div>

</template>

<script>
import { apiKey } from '../../.apiKey.js'
import ArtExpanded from './ArtExpanded.vue'

export default {
  name: 'ArtSection',
  components: {
    ArtExpanded
  },
  data() {
    return {
      artworks: [],
      isExpanded: false,
      imageUrl: '',
      date: '',
      imageid: 0
    }
  },
  methods: {
    getRandomPage() {
      let min = Math.ceil(1)
      let max = Math.floor(9)
      return Math.floor(Math.random() * (max - min)) + min
    },
    fetchArt() {
      fetch(`https://cors-anywhere.herokuapp.com/https://api.harvardartmuseums.org/image?apikey=${apiKey}&size=40&page=${this.getRandomPage()}`)
        .then(response => response.json())
        .then(result => this.artworks = result.records)
        .catch(error => console.log(error.message))
    },
    expandImage($event) {
      this.imageUrl = event.target.src
      if(!event.target.attributes.date){
        this.date = 'No date provided.'
      } else {
        this.date = event.target.attributes.date.value
      }
      this.imageid = event.target.attributes.imageid.value
      this.isExpanded = !this.isExpanded
    }
  },
  mounted() {
    this.fetchArt()
  }
}

</script>

<style scoped>
  .active {
    pointer-events: none;
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    height: 100vh;
    width: 100vw;;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.8);
    -webkit-backdrop-filter: grayscale(1);
    backdrop-filter: grayscale(1);
  }
  .artsection-title,
  .subtitle,
  .loading,
  .generate-text {
    margin:  0px;
    padding: 0px;
  }
  .artsection-title {
    font-size: 40px;
  }
  .loading {
    margin-top: 200px;
  }
  .loading-text {
    font-size: 60px;
  }
  .header {
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 8px;

  }
  .generate {
    border: 1px solid black;
    padding: 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
  }
  .art-list {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
  }
  .art-listitem {
    list-style: none;
  }
  .artwork {
    height: 200px;
    width: 200px;
    border-radius: 25px;
  }
</style>
