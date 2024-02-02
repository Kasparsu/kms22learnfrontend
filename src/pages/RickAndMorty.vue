<script setup>
import axios from 'axios';
import { ref } from 'vue';
let info = ref(null);
let characters = ref(null);
let searchValue = ref('');
let debounce = null;
getCharacter();
function getCharacter() {
    axios.get('https://rickandmortyapi.com/api/character').then(response => {
        console.log(response.data);
        characters.value = response.data.results;
        info.value = response.data.info;
    }).catch(error => {

    });
}

function next() {
    axios.get(info.value.next).then(response => {
        console.log(response.data);
        characters.value = response.data.results;
        info.value = response.data.info;
    }).catch(error => {

    });
}
function prev() {
    axios.get(info.value.prev).then(response => {
        console.log(response.data);
        characters.value = response.data.results;
        info.value = response.data.info;
    }).catch(error => {

    });
}

function search() {
    clearTimeout(debounce);
    debounce = setTimeout(() => {
        axios.get('https://rickandmortyapi.com/api/character/?name=' + searchValue.value).then(response => {
            console.log(response.data);
            characters.value = response.data.results;
            info.value = response.data.info;
        }).catch(error => {
            characters.value = [];
            info.value = null;
        });
    }, 1000);
}

</script>
<template>
    <div class="field has-addons">
        <div class="control is-expanded">
            <input class="input" type="text" v-model="searchValue" @input="search">
        </div>
        <div class="control">
            <a class="button is-info" @click="search">
                Search
            </a>
        </div>
    </div>

    <div class="field has-addons" v-if="info">
        <p class="control">
            <button :disabled="!info.prev" class="button" @click="prev">
                Prev
            </button>
        </p>
        <p class="control">
            <button :disabled="!info.next" class="button" @click="next">
                Next
            </button>
        </p>
    </div>

    <div v-if="characters" class="columns is-multiline mt-3">
        <div v-for="character in characters" class="column is-one-quarter">
            <div class="card">
                <header class="card-header">
                    <p class="card-header-title">
                        {{ character.name }}
                    </p>
                </header>
                <div class="card-image">
                    <figure class="image m-0">
                        <img :src="character.image" alt="Placeholder image">
                    </figure>
                </div>
                <div class="card-content">
                    <div class="content">
                        <table class="table">
                            <tbody>
                                <tr>
                                    <th>status</th>
                                    <td>{{ character.status }}</td>
                                </tr>
                                <tr>
                                    <th>species</th>
                                    <td>{{ character.species }}</td>
                                </tr>
                                <tr>
                                    <th>gender</th>
                                    <td>{{ character.gender }}</td>
                                </tr>
                                <tr>
                                    <th>origin</th>
                                    <td>{{ character.origin.name }}</td>
                                </tr>
                                <tr>
                                    <th>location</th>
                                    <td>{{ character.location.name }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div v-if="!characters" class="content">
        <h1>No Data found</h1>
    </div>
</template>