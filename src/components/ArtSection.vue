<template>
  <div class="ArtSection">
    <h1 class='artsection-title'>Harvard Art Museum</h1>
    <ul class='art-list'>
      <li v-if='artworks.length' v-for='artwork in artworks' :key='artwork.id' class='art-listitem'>
        <img v-bind:src='`${artwork.baseimageurl}`' class='artwork'></img>
      </li>
    </ul>
    <div v-if='!artworks.length' class='loading'>
      <h2 class='loading-text'>Loading...</h2>
    </div>
  </div>
</template>

<script>
import {apiKey} from '../../.apiKey.js'

export default {
  name: 'ArtSection',
  data() {
    return {
      artworks: []
    }
  },
  methods: {
    getRandomPage() {
      let min = Math.ceil(1);
      let max = Math.floor(9);
      return Math.floor(Math.random() * (max - min)) + min;
    },
    fetchArt() {
      fetch(`https://api.harvardartmuseums.org/image?apikey=${apiKey}&size=40&page=${this.getRandomPage()}`)
        .then(response => response.json())
        .then(result => this.artworks = result.records)
        .catch(error => console.log(error.message))
    }
  },
  mounted() {
    this.fetchArt()
  }
}

</script>

<style scoped>
  .artsection-title,
  .loading {
    margin:  0px;
    padding: 0px;
    text-align: center;
  }
  .artsection-title {

  }
  .loading {
    margin-top: 200px;
  }
  .loading-text {
    font-size: 60px;
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
