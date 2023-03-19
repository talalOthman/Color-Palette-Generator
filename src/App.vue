<script setup>
import ColorCard from './components/ColorCard.vue'
import Message from './components/Message.vue'
import Alert from './components/Alert.vue'
import { onMounted, computed, ref, watchEffect } from 'vue'
import axios from 'axios'
import Spinner from './components/Spinner.vue'

const URL = 'http://colormind.io/api/'
const isAlert = ref(false)
const colors = ref([])
const isLoading = ref(true)
const hexColors = computed(() => colors.value.map(color => rgbToHex(...color)))

onMounted(() => {
  onGenerate()
  isLoading.value = true
})

watchEffect(() => {
  document.addEventListener('keydown', (e) => {
    if (e.code === 'Space') {
      onGenerate()
    }
  })
  document.addEventListener('keydown', (e) => {
    if (e.code === 'KeyC') {
      navigator.clipboard.writeText(hexColors.value.join(' '))
      alertUser()
    }
  })
})

const onGenerate = async () => {
  isLoading.value = true
  const response = await axios.post(URL, {
    model: 'default'
  }, {
    headers: {
      'Content-Type': 'text/plain'
    }
  })
  colors.value = response.data.result
  isLoading.value = false
}

const rgbToHex = (r, g, b) => {
  let hex = ((r << 16) | (g << 8) | b).toString(16);
  return "#" + "0".repeat(6 - hex.length) + hex;
}

const alertUser = () => {
  isAlert.value = true

  setTimeout(() => {
    isAlert.value = false
  }, 1000)
}
</script>

<template>
  <div v-if="isLoading" class="flex min-h-screen justify-center items-center">
    <Spinner />
  </div>
  <div v-else class="flex flex-col md:gap-x-4 items-center justify-evenly min-h-screen w-screen gap-y-4 p-3">
    <Alert v-if="isAlert" />
    <h1 class="cursor-default font-bold text-3xl md:text-5xl">Color Pallete Generator</h1>
    <div class="flex flex-col justify-center items-center gap-y-4 md:flex-row md:gap-x-3">
      <div class="flex gap-x-3">
        <ColorCard @alert-event="alertUser" :color="hexColors[0].toUpperCase()" />
        <ColorCard @alert-event="alertUser" :color="hexColors[1].toUpperCase()" />
        <ColorCard @alert-event="alertUser" :color="hexColors[2].toUpperCase()" />
      </div>
      <div class="flex gap-x-3">
        <ColorCard @alert-event="alertUser" :color="hexColors[3].toUpperCase()" />
        <ColorCard @alert-event="alertUser" :color="hexColors[4].toUpperCase()" />
      </div>
    </div>
    <div class="flex flex-col items-center gap-y-3">
      <button @click="onGenerate" class="btn btn-wide btn-primary">Generate Pallete</button>
      <p class="cursor-default hidden md:block">Or just press the "Spacebar" to generate new palettes.</p>
    </div>
    <Message />
  </div>
</template>

