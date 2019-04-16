<template>
  <div class='ArtSection'>
    <header class='header'>
      <h1 class='artsection-title'>Harvard Art Museum Collection</h1>
      <h2 class='subtitle'>♕ Enjoy a random selection of Harvard's finest artwork. ♕</h2>
      <div class='generate' v-on:click='fetchArt()'>
        <p class='generate-text'>New art, please!</p>
      </div>
    </header>
    <ul v-if='artworks.length' class='art-list'>
      <li v-for='artwork in artworks' :key='artwork.id' class='art-listitem'>
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
  <ArtExpanded  v-if='isExpanded'
                :imageUrl='this.imageUrl'
                :date='this.date'
                :imageid='this.imageid'
                @click='isExpanded = true'
                @close='isExpanded = false'
  />
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
    expandImage() {
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
  .ArtSection {
    max-width: 1200px;
    margin: 0 auto;
  }
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
    font-size: 60px;
    font-family: Seaweed Script;
    color: #6b5565;
  }
  .subtitle {
    color: #aa86a1;
  }
  .loading {
    margin-top: 200px;
    text-align: center;
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
    font-size: 26px;
  }
  .generate {
    border: 4px solid #D4A3C8;
    border-radius: 12px;
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 20px;
    padding: 7px 20px;
  }
  .art-list {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    position: relative;
    padding: 0;
  }
  .art-listitem {
    list-style: none;
    padding: 5px;
  }
  .artwork {
    height: 200px;
    width: 200px;
    border-radius: 25px;
    border: 4px solid white;
    object-fit: cover;
    filter: saturate(0.25);
  }
  .artwork:hover {
    transform: scale(1.1, 1.1);
    box-shadow: 5px 5px 5px #646361;
    cursor: pointer;
    filter: saturate(1.6);
    filter: contrast(1.5);
    z-index: 50;
    border: 4px solid #ffbff0;
  }
  .generate:hover {
    cursor: pointer;
    background-color: #c7ccdd;
  }
  .generate:hover p {
    color: white;
    text-shadow: 1px 1px black;
  }
</style>
