<script setup>
  //logica
  import { ref, computed } from 'vue';
  const name = "vue 3";
  const styleColor = "color: orange";
  const arrayColors = ["blue", "red", "orange"];
  const activo = true;
  const mostrar = false;
  const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
  const arrayFrutaNueva = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];
    const counter = ref(0);
    const increment = ()=> counter.value++
    const decrement = () => counter.value--
    const reset = () => counter.value = 0
    const classCounter = computed(()=>{
      if(counter.value > 0){
        return 'positive'
      }else if (counter.value < 0) {
        return 'negative'
      } else {
        return 'zero'
      }
    })
    const arrayFavorite = ref([])
    const add = ()=>{
      arrayFavorite.value.push(counter.value)
    }
    const bloquearbotonAdd = computed(()=>{
      const numSearch = arrayFavorite.value.find(num => num === counter.value)
      if(numSearch === 0) return true
      return numSearch ? true : false
    })
</script>

<template>
  <!-- estructura-->
  <h1>Hola {{ name.toLocaleUpperCase() }}</h1>
  <h2 :style="styleColor">Mi color favorito</h2>
  <h2> {{ arrayColors }}</h2>
  <h2 :style="'color: ${arrayColors[1]}'"></h2>
  <h2>{{ activo ? "Estoy activo" : "Estoy inactivo" }}</h2>
  <h2 v-if="mostrar">hello</h2>
  <h2 v-else>good bye</h2>
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index">{{ fruta }}</li>
  </ul>
  <ul>
    <li v-for="fruta in arrayFrutaNueva" :key="fruta.name">
      {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
    </li>
  </ul>
  <button @click="increment">Aumentar</button>
  <button @click="decrement">Disminuir</button>
  <button @click="reset">Resetear</button>
  <button @click="add" :disabled="bloquearbotonAdd">Agregar</button>
  <h2>{{ counter }}</h2>
  <h2>{{ arrayFavorite }}</h2>
  <ul>
    <li v-for="(num, index) in arrayFavorite" :key="index">{{ num }}</li>
  </ul>
</template>

<style>
/*estilos*/
  h1{
    color: aqua;
  }
  .positive{
    color: green;
  }
  .negative{
    color: red;
  }
  .zero{
    color: black;
  }
</style>