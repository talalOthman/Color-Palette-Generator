<script setup>
import ColorCard from './components/ColorCard.vue'
import Message from './components/Message.vue'
import Alert from './components/Alert.vue'
import { ref } from 'vue'

const isAlert = ref(false)
const alertUser = () => {
  isAlert.value = true

  setTimeout(() => {
    isAlert.value = false
  }, 1000)
}
</script>

<template>
  <div class="flex flex-col md:gap-x-4 items-center justify-evenly min-h-screen w-screen gap-y-4 p-3">
    <Alert v-if="isAlert" />
    <h1 class="cursor-default font-bold text-3xl md:text-5xl">Color Pallete Generator</h1>
    <div class="flex flex-col justify-center items-center gap-y-4 md:flex-row md:gap-x-3">
      <div class="flex gap-x-3">
        <ColorCard @alert-event="alertUser"/>
        <ColorCard @alert-event="alertUser"/>
        <ColorCard @alert-event="alertUser"/>
      </div>
      <div class="flex gap-x-3">
        <ColorCard @alert-event="alertUser"/>
        <ColorCard @alert-event="alertUser"/>
      </div>
    </div>
    <div class="flex flex-col items-center gap-y-3">
      <button class="btn btn-wide btn-primary">Generate Pallete</button>
      <p class="cursor-default hidden md:block">Or just press the "Spacebar" to generate new palettes.</p>
    </div>
    <Message />
  </div>
</template>

