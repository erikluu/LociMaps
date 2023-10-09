<template>
  <selection>
    <div ref="map" class="map"></div>
  </selection>
</template>

<script>
import mapboxgl from 'mapbox-gl'; 

export default {
  data() {
    return {
      pins: [
        {
          longitude: -122.4194,
          latitude: 37.7749,
          color: 'blue' 
        },
        {
          longitude: 0, 
          latitude: 0,
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
        style: {
          version: 8,
          name: "Empty",
          metadata: {
            "mapbox:autocomposite": true,
          },
          glyphs: "mapbox://fonts/mapbox/{fontstack}/{range}.pbf",
          sources: {},
          layers: [
            {
              id: "background",
              type: "background",
              paint: {
                "background-color": "#F5E4CC",
              },
            },
          ],
        },
        zoom: 8,
    });

    this.map = map;
    
    this.map.addControl(new mapboxgl.NavigationControl());

    this.map.on('load', () => {

    //   Add pins
      this.pins.forEach(pin => {
        new mapboxgl.Marker({color: pin.color})
          .setLngLat([pin.longitude, pin.latitude])
          .addTo(this.map);
      });

    });

  }
}
</script>

<style scoped>
  .map {
    position: absolute;
    height: 100%;
    width: 100%;
    z-index: 0;
  }
</style>