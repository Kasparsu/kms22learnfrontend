<template>
    <button class="button is-primary" @click="modalOpen = true">Open Modal</button>
    <Modal :open="modalOpen" @close="modalOpen = false">
        <p class="image is-4by3">
            <img src="https://bulma.io/images/placeholders/1280x960.png" alt="">
        </p>
    </Modal>

    <button class="button is-primary" @click="modalOpen2 = true">Open Modal2</button>
    <Modal :open="modalOpen2" @close="modalOpen2 = false">
        <p class="image is-4by3">
            <img src="http://placekitten.com/1280/960" alt="">
        </p>
    </Modal>

    <button class="button is-primary" @click="modalOpen3 = true">Open Modal3</button>
    <Modal :open="modalOpen3" @close="modalOpen3 = false">
        <p class="image is-4by3">
            <img src="http://placebear.com/1280/960" alt="">
        </p>
    </Modal>
</template>
<script setup>
import { ref } from 'vue';
import Modal from '../components/Modal.vue';
let modalOpen = ref(false);
let modalOpen2 = ref(false);
let modalOpen3 = ref(false);
</script>