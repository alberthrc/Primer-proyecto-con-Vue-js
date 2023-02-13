<script setup>
  import { ref, computed, pushScopeId } from "vue"

    const name = "Vue 3";
    let counter = ref(0);

    const  arrayFavoritos = ref([])

      // Counter ahora es una variable reactiva
    const  increment = () => counter.value++;
    
    const decrement = () =>  counter.value--;

    const reset = () => counter.value = 0;

    const add = () => {
      arrayFavoritos.value.push(counter.value)
    }

    const classCounter = computed(() => {
      if (counter.value === 0) {
        return "zero";
      }
       return counter.value > 0 ? "positive" : "negative";
    });

    const bloquearBtnAdd = computed(() => {
       const numSearch = arrayFavoritos.value.find(num => num === counter.value)
       return numSearch || numSearch === 0;
    });

</script>

<template>
  <div class="container text-center mt-5">
    <h1>Hola {{ name }}</h1>

    <h2 :class="classCounter"> 
      {{  counter }}
    </h2>

    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Click increment</button>
      <button @click="decrement" class="btn btn-danger">Click decrementar</button>
      <button @click="reset" class="btn btn-secondary">Resetear contador</button>
      <button @click="add" :disabled="bloquearBtnAdd"  class="btn btn-primary">Add</button>
    </div>
    

    <h2 class="mt-3">Mis favoritos</h2>
    <ul class="list-group mt-2">
      <li class="list-group-item"
      v-for="(num, index) in arrayFavoritos"
      :key="index">
      {{ num }}

      </li>
    </ul>


  </div>

</template>

<style>
.negative{
  color: red;
}
.positive{
  color: green
}
.zero{
  color: blue;
}
</style>