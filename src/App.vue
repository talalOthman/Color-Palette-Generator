<script setup>
import ColorCard from './components/ColorCard.vue'
</script>

<template>
  <div class="flex flex-col md:gap-x-4 items-center justify-evenly min-h-screen w-screen gap-y-4 p-3">
    <h1 class="font-bold text-3xl md:text-5xl">Color Pallete Generator</h1>
    <div class="flex flex-col justify-center items-center gap-y-4 md:flex-row md:gap-x-3">
    <div class="flex gap-x-3">
      <ColorCard />
      <ColorCard />
      <ColorCard />
    </div>
    <div class="flex gap-x-3">
      <ColorCard />
      <ColorCard />
    </div>
  </div>
  <div class="flex flex-col items-center gap-y-3">
    <button class="btn btn-wide btn-primary">Generate Pallete</button>
    <p class="hidden md:block">Or just press the "Spacebar" to generate new palettes.</p>
  </div>
  </div>
</template>

