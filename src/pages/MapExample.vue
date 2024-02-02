<script setup>
import LeafletMap from '../components/LeafletMap.vue';
import { ref } from 'vue';
let zoom = ref(19);
let center = ref([59.42691, 24.74345]);
</script>

<template>
    <input type="range" min="10" max="20" v-model="zoom">
    <button class="button is-primary" @click="center=[59.41055754000318, 24.605464344508437]">Go To Home</button><br>
    <LeafletMap :center="center" :zoom="zoom"></LeafletMap>
    <LeafletMap :center="[59.41055754000318, 24.605464344508437]" :zoom="14"></LeafletMap>
</template>
