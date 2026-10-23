<script setup>
import { ref, computed, onMounted } from 'vue'
import BuscadorPaises from './components/BuscadorPaises.vue'
import ListaPaises from './components/ListaPaises.vue'

const API_KEY = import.meta.env.API_KEY
const paises = ref([])
const cargando = ref(true)
const error = ref('')
const busqueda = ref('')
const region = ref('')

onMounted(async () => {
  try {
    const url = `https://api.restcountries.com/countries/v5?q=Canada&api-key=${API_KEY}`
    const respuesta = await fetch(url)
    if (!respuesta.ok) throw new Error('Respuesta no válida')
    const datos = await respuesta.json()
    console.log(datos)
    paises.value = datos
  } catch (e) {
    error.value = 'No fue posible obtener los datos de la API'
  } finally {
    cargando.value = false
  }
})



// porfa fredy esto es para que lo filtres 
const filtrados = computed(() => paises.value)
</script>

<template>
  <h1>Explorador de Países</h1>

  <BuscadorPaises v-model:busqueda="busqueda" v-model:region="region" />

  <p v-if="cargando" class="mensaje">Cargando países...</p>
  <p v-else-if="error" class="mensaje">{{ error }}</p>
  <p v-else-if="filtrados.length === 0" class="mensaje">No se encontraron resultados</p>
  <ListaPaises v-else :paises="filtrados" />
</template>