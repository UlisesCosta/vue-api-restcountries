<script setup>
import { computed } from 'vue'

const props = defineProps({ pais: Object })

const capital = computed(() => props.pais?.capitals?.[0]?.name ?? 'Sin capital')
const poblacion = computed(() => props.pais?.population?.toLocaleString('es-MX') ?? 'Sin datos')
const region = computed(() =>
  [props.pais?.region, props.pais?.subregion].filter(Boolean).join(' · ') || 'Sin datos'
)
const superficie = computed(() => {
  const km = props.pais?.area?.kilometers
  return km ? `${km.toLocaleString('es-MX')} km²` : null
})
const idiomas = computed(() => props.pais?.languages?.map((i) => i.name).join(', '))
const monedas = computed(() => props.pais?.currencies?.map((m) => m.name).join(', '))
</script>

<template>
  <article class="tarjeta" v-if="pais">
    <img
      v-if="pais.flag?.url_svg"
      :src="pais.flag.url_svg"
      :alt="`Bandera de ${pais.names.common}`"
    />
    <h2>{{ pais.names.common }}</h2>

    <dl>
      <dt>Capital</dt>
      <dd>{{ capital }}</dd>

      <dt>Región</dt>
      <dd>{{ region }}</dd>

      <dt>Población</dt>
      <dd>{{ poblacion }}</dd>

      <template v-if="superficie">
        <dt>Superficie</dt>
        <dd>{{ superficie }}</dd>
      </template>

      <template v-if="idiomas">
        <dt>Idiomas</dt>
        <dd>{{ idiomas }}</dd>
      </template>

      <template v-if="monedas">
        <dt>Moneda</dt>
        <dd>{{ monedas }}</dd>
      </template>
    </dl>
  </article>
</template>