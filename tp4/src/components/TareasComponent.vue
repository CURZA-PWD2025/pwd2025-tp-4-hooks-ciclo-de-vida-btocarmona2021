<script setup lang="ts">
import type { Tarea } from "@/interface/tarea";
import { onBeforeUpdate, onUpdated, ref } from "vue";
import { Icon } from "@iconify/vue";

const tareas = ref<Tarea[]>([]);
const tareasanteriores = ref<Tarea[]>([]);

const nueva = ref("");

const nuevaTarea = () => {
  if (!nueva.value.trim()) return; // Evita agregar tareas vacías
  const tarea: Tarea = {
    id: tareas.value.length + 1,
    tarea: nueva.value,
    completed: false,
    color: "gray",
  };
  tareas.value.push(tarea);
  nueva.value = "";
};
const completarTarea = (id: number) => {
  tareas.value = tareas.value.map((tarea) => {
    if (tarea.id === id) {
      tarea.completed = !tarea.completed;
      tarea.completed ? tarea.color='#ADFF2F':tarea.color='gray'
    }
    return tarea;
  });
};

onBeforeUpdate(() => {
  console.log("Lista aún no modificada");
});

onUpdated(() => {
  console.log("Lista modificada");
});

</script>

<template>
  <div class="contenedor">
    <button @click="tareas = []" class="btn">limpiar Tareas</button>
    <div class="newtarea">
      <form @submit.prevent="nuevaTarea" class="formulario">
        <textarea
          v-model="nueva"
          class="texto"
          placeholder="Agrega tu nueva tarea"
        ></textarea>
        <button class="btn" type="submit">Nueva Tarea</button>
      </form>
    </div>

    <div 
      v-for="(tarea, index) in tareas"
      :key="index"
      class="tareas animate__animated animate__fadeInLeft animate__duration-1s"
      :style="{ backgroundColor: tarea.color }"
    >
      <label class="tarea">{{ tarea.tarea }}</label>
      <div @click="completarTarea(tarea.id)" class="iconos">
        <Icon
          v-if="tarea.completed"
          icon="mdi:check-bold"
          width="32"
          height="32"
          style="color: green"
        />
        <Icon
          v-else
          icon="mdi:hourglass"
          width="32"
          height="32"
          style="color: darkgrey"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.contenedor {
  width: 500px;
  max-height: 520px;
  overflow: auto;
  background-color: darkslategrey;
  border-radius: 8px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
}

.newtarea {
  width: 90%;
  background-color: darkgoldenrod;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 8px;
}

.formulario {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.texto {
  width: 100%;
  height: 80px;
  padding: 5px;
  background-color: #ffcccc;
  border: none;
  border-radius: 4px;
  resize: none;
}

.btn {
  width: 140px;
  height: 30px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin: 10px 0;
}

.tareas {
  width: 90%;
  background-color: rgb(55, 73, 69);
  margin-bottom: 8px;
  padding: 10px;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 0 3px 1px whitesmoke;
   animation-duration: 0.3s
}

.tarea {
  flex: 1;
  display: flex;
  align-items: center;
}

.iconos {
  width: 40px;
  height: 40px;
  background-color: rgb(146, 37, 146);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
}
.iconos :hover {
  cursor: pointer;
}
</style>
