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
  <div>
    <input v-model="busqueda" type="search" placeholder="Buscar país..." aria-label="Buscar país" autocomplete="off" />
    <select v-model="region" aria-label="Filtrar por región">
    <option value="">Todas las regiones</option>
    <option v-for="r in regiones" :key="r.valor" :value="r.valor">{{ r.nombre }}</option>
    </select>
  </div>
  
</template>