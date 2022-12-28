<script setup>
import {ref, computed} from 'vue';
//metodo - methods

const counter = ref(0);
const arrayFavoritos = ref([]);

const add = () => {
    arrayFavoritos.value.push(counter.value);
}
const increment = () =>{
    counter.value ++;
    }
    const disminuir = ()=>{
        counter.value --;
    }
    const reset = () =>{
        counter.value = 0;
    }
const bloquearBtnAdd = computed(() =>{
    const numSearch = arrayFavoritos.value.find(num => num === counter.value);
    if (numSearch === 0) return true;
    return numSearch ? true : false;
    // return numSearch || numSearch === 0

});

    const classCounter = computed(() => {
        if(counter.value === 0){
            return 'cero';
        }
        if(counter.value > 0){
            return 'positive';
        }
        
        if(counter.value < 0){
            return 'negative';
        }
    });
</script>

<template> 
<div class="container text-center mt-3" >
<h2 :class="classCounter">
    {{ counter }}

</h2>
<div class="btn btn-group">
<button @click="increment" class="btn btn-success">Aumentar</button>
<button @click="disminuir" class="btn btn-danger">Disminuir</button>
<button @click="reset" class="btn btn-secondary">Resetear</button>
<button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
</div>

<ul class="list-group mt-4" >
    <li v-for="(num, index) in arrayFavoritos"
    :key="index" class="list-group-item">
    {{ num }}
</li >
</ul>

</div>

</template>

<style>
h1 {
    color: red;
}
.positive{ color: greenyellow}
.negative{color: red}
.cero{color: peru}
</style>