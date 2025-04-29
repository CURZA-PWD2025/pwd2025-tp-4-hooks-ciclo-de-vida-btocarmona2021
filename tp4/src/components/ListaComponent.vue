<script setup lang="ts">
import { ref ,onMounted } from 'vue';
import { profesiones } from "../data/profesiones";
import type { Profesion } from '@/interface/profesion';
const listaProfesiones = ref<Profesion[]>([]);




onMounted(() => {
  setTimeout(() => {
    listaProfesiones.value = profesiones;
  }, 3000);
});
</script>

<template>
  <div></div>
</template>

<style scoped></style>
