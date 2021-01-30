<template>

  <div id="map">
    <l-map
        :center="getLocation"
        :zoom="zoom"
        @update:zoom="zoomUpdated"
        @update:center="centerUpdated"
        @update:bounds="boundsUpdated"
    >
      <l-tile-layer :url="url"></l-tile-layer>
    </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer} from 'vue2-leaflet';

export default {
  components: {
    LMap,
    LTileLayer,
  },
  props: ['coord'],
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      zoom: 10,
      center: [50.4333, 30.5167],
      bounds: null
    };
  },
  created() {
    let geoLocation = navigator.geolocation
    function getPosition (pos) {
      let coord = pos.coords
      return [coord.latitude, coord.longitude]
    }
   this.center = geoLocation.getCurrentPosition(getPosition)
  },
  computed: {
    getLocation () {
      if(this.coord.length) {
        return this.coord
      } else {
        return this.center
      }
    }
  },
  methods: {
    zoomUpdated (zoom) {
      this.zoom = zoom;
    },
    centerUpdated (center) {
      this.center = center;
    },
    boundsUpdated (bounds) {
      this.bounds = bounds;
    }
  }
}
</script>

<style scoped lang="scss">
@import "../assets/reset.css";
#map{
  width: 100%;
  height: 100%;
}
</style>
