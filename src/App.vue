<template>
  <div id="app">
  <InfoWindow
  @getLocation="getLocation"
  />
    <Map :coord="coord"/>
  </div>
</template>

<script>


import InfoWindow from "@/components/InfoWindow";
import Map from "@/components/Map";
export default {
  name: 'App',
  components: {
    Map,
    InfoWindow
  },
  data () {
    return {
    coord: []
    }
  },
  methods: {
    getLocation (coord) {
      this.coord = [coord.lat, coord.lon]
    }
  }
}
</script>

<style lang="scss">
  #app {
    display: flex;
    height: 100vh;
    width: 100vw;
  }
</style>
