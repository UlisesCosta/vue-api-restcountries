<script setup>
import { computed } from 'vue'

const props = defineProps({ pais: Object })

const capital = computed(() => props.pais?.capitals?.[0]?.name ?? 'Sin capital')
const poblacion = computed(() => props.pais?.population?.toLocaleString('es-MX') ?? 'Sin datos')
</script>

<template>
  <article class="tarjeta" v-if="pais">
    <img 
      v-if="pais.flag?.url_svg" 
      :src="pais.flag.url_svg" 
      :alt="`Bandera de ${pais.name.common}`"
    />
    <h2>{{ pais.name.common }}</h2>
    <p>Capital: {{ capital }}</p>
    <p>Región: {{ pais.region }}</p>
    <p>Población: {{ poblacion }}</p>
  </article>
</template>