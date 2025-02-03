<script setup>
defineProps({
  show: Boolean,
  title: String,
});

const emit = defineEmits(['close', 'submit']);
</script>

<template>
  <div v-if="show" class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50">
    <div class="bg-white p-6 rounded-lg shadow-lg w-96">
      <h2 class="text-xl font-semibold mb-4">{{ title }}</h2>

      <slot></slot>

      <div class="flex justify-end gap-2 mt-4">
        <button 
          class="px-4 py-2 bg-gray-300 rounded-md"
          @click="emit('close')"
        >
          Cancel
        </button>
        <button 
          class="px-4 py-2 bg-blue-500 text-white rounded-md"
          @click="emit('submit')"
        >
          Submit
        </button>
      </div>
    </div>
  </div>
</template>
