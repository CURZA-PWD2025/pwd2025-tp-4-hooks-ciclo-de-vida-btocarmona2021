<script setup lang="ts">

</script>

<template>
  <div class="alerta">
    <slot>
    </slot>
  </div>
</template>

<style scoped>
.alerta{
  width: 80%;
  height: 50px;
  background-color: rgb(29, 116, 29);
  box-shadow: 0 0 3px 2px whitesmoke;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}
</style>