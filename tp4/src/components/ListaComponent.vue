<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { profesiones } from "../data/profesiones";
import type { Profesion } from '@/interface/profesion';
import AlertasComponent from './AlertasComponent.vue';

const listaProfesiones = ref<Profesion[]>([]);
const alerta = ref(false)

onMounted(() => {

  setTimeout(() => {
    alerta.value=true,
    listaProfesiones.value = profesiones;
    setTimeout(() => {
      alerta.value = false;
    },2000)
  }, 3000);
});

</script>

<template>
<div>
  <div v-if="listaProfesiones.length != 0" class="tabla-contenedor animate__animated animate__flipInX">

      <AlertasComponent v-if="alerta">
        <h1>Lista cargada con exito</h1>
      </AlertasComponent>

    <table >
      <caption>Listado de Profesiones</caption>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Descripción</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="profesion in listaProfesiones" :key="profesion.id">
          <td>{{ profesion.id }}</td>
          <td>{{ profesion.nombre }}</td>
          <td>{{ profesion.descripcion }}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <div v-else class="loading-container">
    <img class="cargando" src="/loading.gif" alt="">
    Cargando Datos...
  </div>
</div>
</template>

<style scoped>

.tabla-contenedor {
  margin: 2rem auto;
  padding: 1rem;
  max-width: 800px;
  background-color: #473f3f;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

caption {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  font-weight: bold;
  color: #f5f4f4;
}

thead {
  background-color: #4CAF50;
  color: white;
}

th, td {
  padding: 12px 16px;
  border-bottom: 1px solid #ddd;
}

tr:hover {
  background-color: #01410e;
  cursor: pointer;
}

tbody tr:last-child td {
  border-bottom: none;
}
.cargando{
  width: 100px;
  height: 100px;
}
.loading-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 200px;
}

</style>
