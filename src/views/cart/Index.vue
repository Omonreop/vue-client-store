<script setup>
import axios from "axios";
import ItemCart from "../../components/ItemCart.vue";
import { computed, onMounted, ref } from "vue";

const cartItems = ref([]);
const error = ref(null);
onMounted(async () => {
  try {
    const result = await axios.get(`http://localhost:8000/api/orders/user/1/`);
    let data = Object.assign(
      {},
      ...result.data.map((result) => ({
        cart_items: result.products,
      }))
    );
    cartItems.value = data.cart_items;
  } catch (err) {
    error.value = err.message;
  }
});

const removeFromCart = async (product) => {
  try {
    await axios.delete(
      `http://localhost:8000/api/orders/delete/user/1/product/${product}`
    );
    let indexCart = cartItems.value.map((item) => item.code).indexOf(product);
    cartItems.value.splice(indexCart, 1);
  } catch (error) {
    console.log(error);
  }
};

const totalPrice = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + Number(item.price), 0);
});
</script>
<template>
  <div class="p-6">
    <div class="max-w-4xl mx-auto bg-white shadow-md rounded-lg p-6">
      <h1 class="text-2xl font-bold text-gray-800 mb-4">Shopping Cart</h1>

      <div v-if="cartItems.length" class="space-y-4">
        <ItemCart
          v-for="item in cartItems"
          :key="item.id"
          :item="item"
          v-on:removeItem="removeFromCart($event)"
        />

        <h3 class="text-lg font-semibold text-gray-700 mt-4">
          Total: Rp{{ totalPrice }}
        </h3>

        <button
          id="checkout-button"
          class="w-full bg-indigo-600 text-white py-2 rounded-lg hover:bg-indigo-700 transition duration-300"
        >
          Checkout
        </button>
      </div>

      <p v-else class="text-center text-gray-500">Your cart is empty.</p>
    </div>
  </div>
</template>

<style scoped>
h1 {
  border-bottom: 1px solid #41b883;
  margin: 0;
  margin-top: 16px;
  padding: 16px;
}
#total-price {
  padding: 16px;
  text-align: right;
}
#checkout-button {
  width: 100%;
}
</style>
