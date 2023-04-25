<template>
<div id="map"></div>
</template>

<script>
/* eslint-disable no-undef */
import $ from 'jquery';

import { Loader } from '@googlemaps/js-api-loader';
import { onMounted } from 'vue';
const GOOGLE_MAPS_APIT_KEY = 'AIzaSyCu3V5RB6o45PDnQk38ALiiVTAJ8dT5H14'

export default {
name: 'TheMap.vue',
setup() {
  const loader = new Loader({apiKey: GOOGLE_MAPS_APIT_KEY})
  onMounted(async () => {
      await loader.load()
      google
  })
},
data() {
  return {
  marker: null,
  };
},
mounted() {
  this.initMap();
  window.initMap = this.initMap;
},
methods: {
  initMap() {
  $.ajax({
    url: '../php/db_query_gps.php',
    type: 'POST',
    dataType: 'json',
    success: (result) => {
      const latitude = result.lat;
      const longitude = result.lng;
      const localizacao = new google.maps.LatLng(latitude, longitude);

      map = new google.maps.Map(document.getElementById('map'), {
        zoom: 16,
        center: localizacao,
        heading: 89,
        mapId: '90f87356969d889c',
      });

      const icon = {
        url: '../assets/DT1.png',
        scaledSize: new google.maps.Size(50, 50),
        origin: new google.maps.Point(0, 0),
        anchor: new google.maps.Point(25, 25),
      };

      this.marker = new google.maps.Marker({
        position: localizacao,
        map,
        icon,
        title: 'DT2',
      });
    },
    });

    setInterval(() => {
      $.ajax({
      url: '../php/db_query_gps.php',
      type: 'POST',
      dataType: 'json',
      success: (result) => {
          const latitude = result.lat;
          const longitude = result.lng;
          const localizacao = new google.maps.LatLng(latitude, longitude);

          this.marker.setPosition(localizacao);
        },
      });
    }, 1000);
    },
},
};
</script>

<style scoped>
#map {
height: 100%;
}
</style>