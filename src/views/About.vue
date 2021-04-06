<template>
  <div class="home">
    <div id="map"></div>
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl/dist/mapbox-gl.js";
export default {
  mounted: function () {
    this.createMap();
  },

  methods: {
    createMap: function () {
      mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
      var map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11",
        center: [-74.5, 40],
        zoom: 9,
      });
      var marker1 = new mapboxgl.Marker().setLngLat([-74.5, 40]).addTo(map);
      // create the popup
      var popup = new mapboxgl.Popup({ offset: 25 }).setText("This is not actually where the Washington Monument is.");

      // create DOM element for the marker
      var el = document.createElement("div");
      el.id = "marker";

      // create the marker
      new mapboxgl.Marker(el)
        .setLngLat([-74.6, 40])
        .setPopup(popup) // sets a popup on this marker
        .addTo(map);
      console.log(marker1);
      console.log(map);
    },
  },
};
</script>

<style>
#map {
  height: 500px;
  width: auto;
}
#marker {
  background-image: url("https://docs.mapbox.com/mapbox-gl-js/assets/washington-monument.jpg");
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>
