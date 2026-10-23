<script setup>
const busqueda = defineModel('busqueda')
const region = defineModel('region')

const regiones = [
  { valor: 'Africa', nombre: 'África' },
  { valor: 'Americas', nombre: 'América' },
  { valor: 'Asia', nombre: 'Asia' },
  { valor: 'Europe', nombre: 'Europa' },
  { valor: 'Oceania', nombre: 'Oceanía' },
  { valor: 'Antarctic', nombre: 'Antártida' },
]
</script>

<template>
  <input v-model="busqueda" placeholder="Buscar país..." />
  <select v-model="region">
    <option value="">Todas las regiones</option>
    <option v-for="r in regiones" :key="r.valor" :value="r.valor">{{ r.nombre }}</option>
  </select>
</template>