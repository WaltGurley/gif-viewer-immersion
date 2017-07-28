<template>
  <div class="gif-holder">
    <div v-for="gif in gifSubject" class="img-holder">
      <img v-bind:src="gif.images.original.url" alt="" class="gif-img">
    </div>
    <!-- {{ gifSubject[0].images.fixed_height.url }} -->
  </div>
</template>

<script>
export default {
  name: 'gif-holder',
  props: ['gifSubject'],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  $immersion-width: 6816px;
  $immersion-height: 2240px;

  $tile-width: 426px;
  $tile-height: 320px;

  $grid-columns: 16;
  $grid-rows: 7;

  .gif-holder {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: flex-start;
    width: $tile-width * 13;
    height: 100%;

    .img-holder {
      height: $tile-height;

      .gif-img {
        height: 100%;
      }
    }
  }
</style>
