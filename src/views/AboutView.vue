<template>
  <div class="about">
    <div id="map"></div>
  </div>
</template>
<style>
body {
  margin: 0;
  padding: 0;
}
#map {
  height: 500px;
  width: 100%;
}
</style>
<script>
/* global mapboxgl */
export default {
  data: function () {
    return {
      places: [
        { lat: -25.363, lng: 131.044, description: "A place in Australia" },
        { lat: -33.8675, lng: 151.207, description: "The main city!" },
      ],
    };
  },
  methods: {},
  mounted() {
    mapboxgl.accessToken = process.env.VUE_APP_MY_API_KEY;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/streets-v11", // style URL
      center: [this.places[0].lng, this.places[0].lat], // starting position [lng, lat]
      zoom: 8, // starting zoom
    });

    this.places.forEach((place) => {
      const popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
      new mapboxgl.Marker().setLngLat([place.lng, place.lat]).setPopup(popup).addTo(map);
    });
    console.log(map);
  },
};
</script>
