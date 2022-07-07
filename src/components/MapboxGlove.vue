<template>
    <div class="map-container" ref="mapContainer">

    </div>
</template>

<script setup lang="ts">
import "mapbox-gl/dist/mapbox-gl.css";
import mapboxgl from "mapbox-gl"; // or "const mapboxgl = require('mapbox-gl');"
import { onMounted, ref } from "vue";

mapboxgl.accessToken =
    "pk.eyJ1Ijoia2lrb25ldGEiLCJhIjoiY2toY2ZodDlrMDZwMzJ0bXB6N3pnbnFxeSJ9.NU45fbFBqQvO0vsEMaXh_Q";

const mapContainer = ref<HTMLElement>();

onMounted(() => {
    const map = new mapboxgl.Map({
        container: mapContainer.value!, // container ID
        style: "mapbox://styles/mapbox/streets-v11", // style URL
        center: [-0.37, 39.46], // starting position [lng, lat]
        zoom: 12, // starting zoom
        projection: "globe", // display the map as a 3D globe
    } as any);

    map.on('style.load', () => {
        map.setFog({
            color: 'rgb(186, 210, 235)', // Lower atmosphere
            'high-color': 'rgb(36, 92, 223)', // Upper atmosphere
            'horizon-blend': 0.02, // Atmosphere thickness (default 0.2 at low zooms)
            'space-color': 'rgb(11, 11, 25)', // Background color
            'star-intensity': 0.6 // Background star brightness (default 0.35 at low zoooms )
        } as any );
    });

})


</script>

<style scoped>
.map-container {
    height: 100vh;
    width: 100vw;
}
</style>
