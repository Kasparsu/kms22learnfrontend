<script setup>
import axios from 'axios';
import { ref } from 'vue';
let weather = ref(null);
let searchValue = ref('tallinn');
let lastSearchValue = ref('');
search();

function search(){
    lastSearchValue.value = searchValue.value;
    axios.get('https://goweather.herokuapp.com/weather/' + searchValue.value).then(response => {
        console.log(response.data);
        weather.value = response.data;
    }).catch(error => {
        
    });
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
    <div v-if="weather && weather.temperature" class="card">
        <div class="card-content">
            <div class="content">
                <h1>{{ lastSearchValue.charAt(0).toUpperCase() + lastSearchValue.slice(1).toLowerCase() }}</h1>
                <table class="table">
                    <tbody>
                        <tr>
                            <th>Temp</th>
                            <td>{{ weather.temperature }}</td>
                        </tr>
                        <tr>
                            <th>Wind</th>
                            <td>{{ weather.wind }}</td>
                        </tr>
                        <tr>
                            <th>Description</th>
                            <td>{{ weather.description }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <div v-if="weather && weather.temperature" class="columns mt-3">
        <div v-for="forecast in weather.forecast" class="column">
            <div class="card">
                <div class="card-content">
                    <div class="content">
                        <h1>In {{ forecast.day }}
                            <span v-if="forecast.day > 1">
                                days
                            </span>
                            <span v-else>
                                day
                            </span>
                        </h1>
                        <table class="table">
                            <tbody>
                                <tr>
                                    <th>Temp</th>
                                    <td>{{ forecast.temperature }}</td>
                                </tr>
                                <tr>
                                    <th>Wind</th>
                                    <td>{{ forecast.wind }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div v-if="!weather || !weather.temperature" class="content">
        <h1>No Data found</h1>
    </div>
</template>