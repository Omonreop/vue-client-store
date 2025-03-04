<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import NotFound from "../errors/404.vue";

const product = ref({});
const error = ref(null);
const notif = ref(false);
const route = useRoute();

onMounted(async () => {
  try {
    const code = route.params.id;
    const result = await axios.get(
      `http://localhost:8000/api/products/${code}`
    );
    product.value = result.data;
  } catch (err) {
    error.value = err.message;
  }
});

const addToCart = async (product) => {
  try {
    await axios.post("http://localhost:8000/api/orders/update/user/1/", {
      product: product,
    });
    notif.value = true;
  } catch (error) {
    error.value = error.message;
  }
};
</script>
<template>
  <div class="p-6">
    <p v-if="error" class="text-center text-red-500">Error: {{ error }}</p>

    <div
      v-if="product"
      class="max-w-4xl mx-auto bg-white shadow-md rounded-lg p-6 flex flex-col md:flex-row gap-6"
    >
      <h4 v-if="notif" class="text-green-600 font-semibold text-center">
        Item added successfully
      </h4>

      <div class="md:w-1/2 flex justify-center">
        <img
          :src="`http://localhost:8000${product.imageUrl}`"
          alt="Product Image"
          class="w-full h-80 object-cover rounded-md"
        />
      </div>

      <div class="md:w-1/2 space-y-4">
        <h1 class="text-2xl font-bold text-gray-800">{{ product.name }}</h1>
        <h3 class="text-xl font-semibold text-slate-900">
          Rp{{ product.price }}
        </h3>
        <p class="text-gray-600">Average Rating: {{ product.averageRating }}</p>

        <button
          @click="addToCart(product.code)"
          class="w-full bg-slate-900 text-white py-2 rounded-lg hover:bg-slate-200 transition duration-300"
        >
          Add to Cart
        </button>

        <p class="text-gray-700 text-justify">{{ product.description }}</p>
      </div>
    </div>

    <NotFound v-else />
  </div>
</template>
