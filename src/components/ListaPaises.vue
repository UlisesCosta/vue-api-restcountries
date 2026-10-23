<script setup>
import TarjetaPais from './TarjetaPais.vue'
defineProps({ paises: Array })
</script>

<template>
<div class="lista">
<TarjetaPais v-for="pais in paises" :key="pais.codes.alpha_3" :pais="pais" />
</div>
</template>