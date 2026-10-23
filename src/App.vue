<script setup>
import { ref, computed, onMounted } from 'vue'
import BuscadorPaises from './components/BuscadorPaises.vue'
import ListaPaises from './components/ListaPaises.vue'

const API_KEY = import.meta.env.API_KEY
const URL_API = 'https://api.restcountries.com/countries/v5'

const paises = ref([])
const cargando = ref(true)
const error = ref('')
const busqueda = ref('')
const region = ref('')

const cargar = async (params) =>  {
  cargando.value = true
  error.value = ''
  try {
    const respuesta = await fetch(`${URL_API}?q=${encodeURIComponent(consulta)}`, {
      headers: { Authorization: `Bearer ${API_KEY}` },
    })
    if (!respuesta.ok) throw new Error('Respuesta no valida de la api')
    const json = await respuesta.json()
    paises.value = json.data?.objects ?? []
  } catch (e) {
    paises.value = []
    error.value = 'Fallo al recuperar datos'
  } finally {
    cargando.value = false
  }
}

onMounted(() => cargar('Mexico'))



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