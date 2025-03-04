<template>
  <div class="flex items-center bg-white shadow-md rounded-lg p-4 gap-4">
    <img
      :src="`http://localhost:8000${item.imageUrl}`"
      alt="Product Image"
      class="w-24 h-24 object-cover rounded-md"
    />
    <div class="flex-1">
      <h3 class="text-lg font-semibold text-gray-800">{{ item.name }}</h3>
      <p class="text-indigo-600 font-bold">Rp{{ item.price }}</p>
    </div>
    <button
      @click="$emit('removeItem', item.code)"
      class="bg-red-500 text-white px-4 py-2 rounded-lg hover:bg-red-600 transition duration-300"
    >
      Remove
    </button>
  </div>
</template>

<script setup>
defineProps(["item"]);
</script>

<style scoped>
.product-container {
  align-content: "center";
  border-bottom: 1px solid #ddd;
  display: flex;
  padding: 16px;
  width: 100%;
}
.product-image {
  flex: 1;
  height: 100px;
  max-width: 100px;
}
.details-wrap {
  padding: 0 16px;
  flex: 3;
}
.remove-button {
  flex: 1;
  margin: auto;
}
</style>
