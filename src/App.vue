<template>
  <div id="app">
    <div class="search-fields">
      <h1>Bunch-O-Kitties 2.0</h1>
      <h2>GIF stress</h2>
      <input type="text" v-model="searchTerm" placeholder="Search Term">
      <button type="button" name="button" v-on:click="searchGif">Search</button>
    </div>
    <gif-holder v-bind:gifSubject="searchResponse"></gif-holder>
    <div class="test-wrapper"></div>
  </div>
</template>

<script>
import GifHolder from './components/GifHolder'
import _ from 'lodash'

const key = '28a10c5337904e8fa4f600bda2469814'
const ranOffset = _.random(0, 91)

export default {
  name: 'app',
  components: {
    GifHolder
  },
  data () {
    return {
      searchTerm: '',
      searchResponse: []
    }
  },
  methods: {
    searchGif () {
      fetch(
        'https://api.giphy.com/v1/gifs/search?api_key=' + key +
        '&q=' + this.searchTerm + '&limit=91&offset=' + ranOffset + '&rating=G&lang=en'
      )
      .then(response => response.json())
      .then(data => { this.searchResponse = _.shuffle(data.data) })
    }
  },
  mounted () {
    fetch(
      'https://api.giphy.com/v1/gifs/search?api_key=' + key +
      '&q=kittens&limit=91&offset=' + ranOffset + '&rating=G&lang=en'
    )
    .then(response => response.json())
    .then(data => { this.searchResponse = _.shuffle(data.data) })
  }
}
</script>

<style lang="scss">
#app {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: row;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fad1d1;
  background-color: #222;
}

$immersion-width: 6816px;
$immersion-height: 2240px;

$tile-width: 426px;
$tile-height: 320px;

$grid-columns: 16;
$grid-rows: 7;

.search-fields {
  height: 100%;
  width: $tile-width * 3;
  font-size: 5vh;

  input, button {
    font-size: 5vh;
  }
}

.test-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: $immersion-width;
  height: $immersion-height;
  z-index: 666;

  pointer-events: none;

  .transparent-image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: $immersion-width;
    height: $immersion-height;
    background-image: image-url("immersion/immersion-test.jpg");
    opacity: 0.25;
  }

  .tile {
    box-sizing: border-box;
    border-color: #000;
    border-width: 1px;
    border-style: solid;
    background-color: none;
  }

  @for $i from 1 through ($grid-columns * $grid-rows) {
    .tile-#{$i - 1} {
      width: $tile-width;
      height: $tile-height;
      float: left;
    }
  }
}
</style>
