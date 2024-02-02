<script setup>
import * as L from 'leaflet';
import 'leaflet/dist/leaflet.css';
import { onMounted, watch,getCurrentInstance, ref } from 'vue';
import 'leaflet/dist/images/marker-shadow.png';
const instance = getCurrentInstance()
const uuid = ref(instance.uid)
const props = defineProps(['center', 'zoom']);
let map;
onMounted(()=> {
    map = L.map('map'+uuid.value).setView(props.center, props.zoom);
    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
    }).addTo(map);
    let marker = L.marker([59.42691, 24.74345]).addTo(map);
});

watch(() => props.zoom, (newZoom) => {
    map.flyTo(props.center,newZoom);
});

watch(() => props.center, (newCenter) => {
    map.flyTo(newCenter, props.zoom);
});
</script>

<template>
 <div :id="'map'+uuid"></div>
</template>
<style scoped>
div {
    height: 600px;
}
</style>