<script setup>
import { reactive, ref } from 'vue';
import Card from './components/Card.vue';
import Modal from './components/Modal.vue';

const items = reactive([{
  id: 1,
  name: 'Test Name',
  description: 'This is a test description.',
  imgSrc: 'https://www.thecookierookie.com/wp-content/uploads/2023/04/featured-stovetop-burgers-recipe.jpg',
}]);
const isFormOpen = ref(false);
const selectedItem = ref(null);

const handleSubmit = () => {
  if (selectedItem.value.id) {
    // Updating existing item
    const index = items.findIndex(i => i.id === selectedItem.value.id);
    if (index !== -1) {
      items[index] = { ...selectedItem.value };
    }
  } else {
    // Adding new item
    const newItem = { ...selectedItem.value, id: items.length + 1 };
    items.push(newItem);
  }

  isFormOpen.value = false; // Close modal
};

const openAddModal = () => {
  selectedItem.value = { id: null, name: '', description: '', imgSrc: '' };
  isFormOpen.value = true;
};

const openUpdateModal = (item) => {
  selectedItem.value = { ...item };
  isFormOpen.value = true;
};

const removeItem = (id) => {
  const index = items.findIndex(i => i.id === id);
  if (index !== -1) {
    items.splice(index, 1);
  }
};

</script>

<template>
  <div class="min-h-screen bg-gray-100">
    <header class="bg-primary text-white py-4 shadow-md">
      <div class="container mx-auto flex items-center justify-between px-4">
        <div class="text-xl font-semibold">My Tailwind Vue App</div>
        <button class="bg-white text-primary px-4 py-2 rounded-md shadow hover:bg-gray-200" @click="openAddModal">
          Add Item
        </button>
      </div>
    </header>

    <main class="flex justify-center items-center py-10">
      <div class="grid gap-4 justify-center 
                  grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4
                  px-4">
        <Card v-for="item in items" :key="item.id" :item="item" @update-item="openUpdateModal" @remove-item="removeItem"/>
      </div>
    </main>

    <!-- Modal Component -->
    <Modal 
      :show="isFormOpen"
      title="Add Item"
      @close="isFormOpen = false"
      @submit="handleSubmit"
    >
      <form @submit.prevent="handleSubmit">
        <div class="mb-4">
          <label class="block text-gray-700">Name:</label>
          <input 
            v-model="selectedItem.name" 
            type="text" 
            class="w-full px-3 py-2 border rounded-md"
            required
          />
        </div>

        <div class="mb-4">
          <label class="block text-gray-700">Description:</label>
          <textarea 
            v-model="selectedItem.description" 
            class="w-full px-3 py-2 border rounded-md"
            required
          ></textarea>
        </div>

        <div class="mb-4">
          <label class="block text-gray-700">Image URL:</label>
          <input 
            v-model="selectedItem.imgSrc" 
            type="text" 
            class="w-full px-3 py-2 border rounded-md"
            required
          />
        </div>
      </form>
    </Modal>
  </div>
</template>
