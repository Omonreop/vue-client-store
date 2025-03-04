<template>
  <div
    class="bg-white rounded-lg shadow-md p-4 hover:shadow-lg transition duration-300"
  >
    <img
      :src="`http://localhost:8000${product.imageUrl}`"
      alt="Product Image"
      class="w-full h-48 object-cover rounded-md mb-4"
    />
    <h3 class="text-lg font-semibold text-gray-800 mb-2">{{ product.name }}</h3>
    <p class="text-indigo-600 font-bold mb-3">Rp{{ product.price }}</p>
    <RouterLink :to="{ name: 'product-detail', params: { id: product.code } }">
      <button
        class="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700 transition duration-300"
      >
        Detail
      </button>
    </RouterLink>
  </div>
</template>

<script setup>
defineProps(["product"]);
</script>
