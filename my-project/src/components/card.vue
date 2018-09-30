<template>
  <div class="vital-chart-wx">
    <div class="my-charts">
      <ec-canvas  class="canvas" id="mychart" canvas-id="mychart-bar" :ec="ec"></ec-canvas>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['options'],
    data () {
      return {
        ec: {
          options: this.options
        }
      }
    },
    watch: {
      options: {
//        handler (newValue, oldValue) {
//          this.getOptions(newValue)
//        },
//        deep: true
      }
    },
    created () {
    },
    mounted () {
    },
    methods: {
      getOptions: function (newValue) {
//        this.ec.options = newValue
      }
    }
  }
</script>

<style>
  .my-charts{
    height: 300px;
  }
  ec-canvas {
    width: 80px;
    height: 80px;
  }
</style>
