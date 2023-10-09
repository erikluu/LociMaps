<template>
  <div ref="map"></div>
</template>

<script>
import mapboxgl from 'mapbox-gl'; 

export default {
  data() {
    return {
      map: null,
      pins: [
        {
          longitude: -122.4194,
          latitude: 37.7749,
          color: 'blue' 
        },
        {
          longitude: -43.2654, 
          latitude: -22.9068,
          color: 'red'
        }
      ]
    }
  },
  mounted() {
    console.log(import.meta.env.VITE_MAPBOX_ACCESS_TOKEN)
    mapboxgl.accessToken = import.meta.env.VITE_MAPBOX_ACCESS_TOKEN

    const map = new mapboxgl.Map({
        container: this.$refs.map,
        style: "mapbox://styles/mapbox/streets-v12", // Replace with your preferred map style
        center: [-71.224518, 42.213995],
        zoom: 9,
    });

    this.map = map;
    
    // Add navigation controls 
    this.map.addControl(new mapboxgl.NavigationControl());

    this.map.on('load', () => {

    //   Add pins
      this.pins.forEach(pin => {
        new mapboxgl.Marker({color: pin.color})
          .setLngLat([pin.longitude, pin.latitude])
          .addTo(this.map);
      });

    //   Add land 
      this.map.addSource('land', {
        type: 'geojson',
        data: 'https://docs.mapbox.com/mapbox-gl-js/assets/ne_110m_land.geojson'
      });

      this.map.addLayer({
        id: 'land',
        type: 'fill',
        source: 'land',
        layout: {},
        paint: {
          'fill-color': '#f08a24' 
        }
      });

    });

  }
}
</script>

<style scoped>
  .map-container {
    position: absolute;
    height: 100vh;
    z-index: 0;
  }
</style>