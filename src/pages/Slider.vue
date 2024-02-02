<script setup>
import bulmaCarousel from 'bulma-carousel/src/js/index.js';
import { onMounted } from 'vue';
onMounted(() => {
    bulmaCarousel.attach('#carousel-demo', {
			slidesToScroll: 1,
			slidesToShow: 1,
            infinite: true,
            autoplay: true
	});
});
</script>

<template>
    <div id="carousel-demo" class="carousel">
        <div class="item-1">
            <p class="image is-4by3">
                <img src="http://placekitten.com/1280/960" alt="">
            </p>
        </div>
        <div class="item-2">
            <p class="image is-4by3">
                <img src="https://bulma.io/images/placeholders/1280x960.png" alt="">
            </p>
        </div>
        <div class="item-3">
            <p class="image is-4by3">
                <img src="http://placebear.com/1280/960" alt="">
            </p>
        </div>
    </div>
</template>