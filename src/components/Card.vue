<script setup>
import { ref, computed } from 'vue';

const props = defineProps(['item']);

console.log(props.item)

const name = computed(() => {
  return props.item.name;
})
const description = computed(() => {
  return props.item.description;
})
const imageSrc = computed(() => {
  return props.item.imgSrc;
})

const emit = defineEmits(['update-item', 'remove-item']);
</script>

<template>
  <div class="relative max-w-sm rounded-xl shadow-lg bg-white p-4 border border-gray-200">
    <button 
      @click="emit('remove-item', props.item.id)"
      class="absolute top-2 right-2 bg-gray-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-sm hover:bg-gray-600 transition shadow-md"
    >
      &times;
    </button>

    <img class="w-full rounded-lg aspect-square object-cover object-center" :src="imageSrc" alt="Card Image">

    <div class="p-4">
      <h2 class="text-xl font-semibold text-primary">{{ name }}</h2>
      <p class="text-gray-600 mt-2">{{ description }}</p>
      <button class="mt-4 bg-secondary text-white px-4 py-2 rounded-lg hover:bg-secondary-600 transition" @click="emit('update-item', props.item)">
        Update
      </button>
    </div>
  </div>
</template>

<style scoped>
</style>
