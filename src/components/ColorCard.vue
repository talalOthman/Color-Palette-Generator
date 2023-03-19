<script setup>
defineEmits(['alertEvent'])
defineProps(['color'])
</script>

<template>
    <div @click="$emit('alertEvent')" class="cursor-pointer border flex flex-col items-center h-40 w-28 md:h-64 md:w-40 p-1 rounded-md bg-white text-gray-600">
        <div class="bg-purple-600 h-60 w-full rounded-md" :style="{ 'background-color': color }"></div>
        <div class="flex items-center justify-center w-full h-10">
            <p class="font-bold">{{ color }}</p>
        </div>
    </div>
</template>