<script setup>
import { RouterLink, RouterView } from 'vue-router'
import "bootstrap/dist/css/bootstrap.min.css";
import BarraNavegacao from './componentes/BarraNavegacao.vue';
import './complementos/estilos.css'

</script>

<template>
  <BarraNavegacao></BarraNavegacao>

  <RouterView></RouterView>
</template>

<style scoped>
</style>
