<template>
  <div class="gif-holder">
    <div v-for="gif in gifSubject" class="img-holder">
      <img v-bind:src="gif.images.downsized.url" alt="" class="gif-img">
    </div>
  </div>
</template>

<script>
export default {
  name: 'gif-holder',
  props: ['gifSubject'],
  data () {
    return {
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

  $demo-wall-width: 3840px;
  $demo-wall-height: 2160px;

  $grid-columns: 16;
  $grid-rows: 7;

  .gif-holder {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: flex-start;
    height: 100%;

    @media (width: 6816px) {
      width: $tile-width * 13;
    }

    @media (width: 3840px) {
      width: $demo-wall-width;
    }

    .img-holder {

      @media (width: 6816px) {
        height: $tile-height;
        width: $tile-width;
      }

      @media (width: 3840px) {
        width: $demo-wall-width / 10;
        height: $demo-wall-height / 8;
      }

      .gif-img {
        height: 100%;
        width: 100%;
        object-fit: cover;
      }
    }
  }
</style>
