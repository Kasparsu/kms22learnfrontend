<template>
    <div class="container">
        <div class="content mt-3">
            <div class="field has-addons">
                <div class="control is-expanded">
                    <input class="input" type="text" v-model="message" @keydown.enter="addItem">
                </div>
                <div class="control">
                    <button class="button is-info" @click="addItem">
                        Add item
                    </button>
                </div>
            </div>

            <ItemList :items="items" title="All Items"></ItemList>
            <ItemList :items="doneItems" title="Done Items"></ItemList>
            <ItemList :items="toDoItems" title="ToDo Items"></ItemList>
        </div>
    </div>
</template>
<script setup>
import { ref, computed } from 'vue';
import ItemList from './components/ItemList.vue';

let message = ref('');
let i = 0;
let items = ref([
    {id: i++, name:'Sai', isDone: false},
    {id: i++, name:'Piim', isDone: true},
    {id: i++, name:'Viin', isDone: false},
]);
function addItem(){
    if(message.value.trim() !== ''){
        items.value.push({id: i++, name: message.value.trim(), isDone: false});
    }
    message.value = '';
}
const doneItems = computed(() => {
    return items.value.filter(item => item.isDone);
});
const toDoItems = computed(() => {
    return items.value.filter(item => !item.isDone);
});
</script>