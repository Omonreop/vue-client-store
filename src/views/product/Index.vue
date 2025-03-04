<script setup>
import axios from "axios";
import ProductItem from "../../components/ProductItem.vue";
import { onMounted, ref } from "vue";

const products = ref([]);
const loading = ref(true);
const error = ref(null);

onMounted(async () => {
  try {
    const result = await axios.get("http://localhost:8000/api/products");
    products.value = result.data;
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
});
</script>
<template>
  <div class="p-6">
    <p v-if="loading" class="text-center text-gray-500">Loading...</p>
    <p v-if="error" class="text-center text-red-500">Error: {{ error }}</p>
    <div
      v-else
      class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6"
    >
      <ProductItem
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>
