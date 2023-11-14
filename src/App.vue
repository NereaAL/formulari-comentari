<script setup lang="ts">
import Formulari from "./components/Formulari.vue";
import Enviat from "./components/Enviat.vue";
import type Entry from "./types/Entry";
import { reactive } from "vue";

const entrades: Entry[] = reactive([])

const manipularPost = (entradaPost: Entry) => {

  entrades.push(entradaPost)
  console.log(entradaPost)
}



</script>

<template>
  <div class="principal">
    <!-- les dues arrobes ajuden per distinguir els events personalitzats -->
    <Formulari @@create="manipularPost"></Formulari>
  </div>
  <ul>
    <!-- enviat com a component ha de rebre les coses que ha d'enviar -->
    <li v-for="entrada in entrades" :key="entrada.id"><Enviat></Enviat></li>
  </ul>
  
</template>

<style scoped>
.principal{
  width: 800px;
}
</style>
