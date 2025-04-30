<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";

const alto = ref(window.innerHeight);
const ancho = ref(window.innerWidth);

const actualizaDimension = () => {
  alto.value = window.innerHeight;
  ancho.value = window.innerWidth;
};

onMounted(() => {
  window.addEventListener("resize", actualizaDimension);
});

onUnmounted(() => {
  window.removeEventListener("resize", actualizaDimension);
});
</script>

<template>
  <div class="dimensiones-container">
    <h2 class="titulo">Dimensiones del Componente</h2>
    <div class="dimension">
      <h3 class="label">Alto:</h3>
      <p class="valor">{{ alto }} px</p>
    </div>
    <div class="dimension">
      <h3 class="label">Ancho:</h3>
      <p class="valor">{{ ancho }} px</p>
    </div>
  </div>
</template>

<style scoped>
.dimensiones-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 10px;
  width: 300px;
  margin: 50px auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.titulo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
}

.dimension {
  margin-bottom: 15px;
}

.label {
  font-size: 1rem;
  color: #555;
}

.valor {
  font-size: 1.2rem;
  font-weight: 500;
  color: #007bff;
  margin-top: 5px;
}
</style>
