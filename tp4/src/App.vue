<script setup lang="ts">
import ListaComponent from "@/components/ListaComponent.vue";
import TareasComponent from "./components/TareasComponent.vue";
import DimensionComponent from "./components/DimensionComponent.vue";
import AlertasComponent from "./components/AlertasComponent.vue";
import { ref } from "vue";

const componentes = { ListaComponent, TareasComponent, DimensionComponent };
const indice = ref();
const componenteActual = ref(AlertasComponent);

const change = (componente: any) => {
  componenteActual.value = componente;
};

</script>

<template>
  <div class="contenedor-principal">
    <div class="botonera">
      <button
        v-for="(comp, nombre) in componentes"
        :key="nombre"
        class="boton"
        @click="change(comp)"
      >
        {{ nombre.replace('Component' , '') }}
      </button>
    </div>

    <div class="componente-contenedor">
      <transition
        mode="out-in"
        enter-active-class="animate__animated animate__flipInY"
      >
        <component :is="componenteActual">
        <h1>Bienvenidos</h1>
        </component>
      </transition>
    </div>
  </div>
</template>

<style scoped>
@import url(https://fonts.googleapis.com/css?family=Chakra+Petch:300,300italic,regular,italic,500,500italic,600,600italic,700,700italic);

.animate__animated{
 --animate-duration: 0.5s;
}

h1{
  color: wheat;
}
.contenedor-principal {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  font-family: chakra petch, sans-serif;
}

.botonera {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}

.boton {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s;
}

.boton:hover {
  background-color: #0056b3;
}


.componente-contenedor {
  width: 100%;
  padding: 20px;

  border-radius: 10px;
  box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.1);
}
</style>
