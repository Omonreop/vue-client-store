<script setup>
import { RouterLink } from "vue-router";
</script>
<template>
  <!-- <div class="">
    <RouterLink :to="{ name: 'product' }" id="products-link"
      ><h1>VUEStore</h1></RouterLink
    >
    <RouterLink :to="{ name: 'cart' }" id="cart-link"
      ><button>Cart</button></RouterLink
    >
  </div> -->
  <div
    class="flex items-center justify-between bg-white shadow-md p-4 ps-7 pe-7"
  >
    <RouterLink
      :to="{ name: 'product' }"
      class="text-2xl font-bold text-slate-900 hover:text-slate-200 transition duration-300"
    >
      VUEStore
    </RouterLink>
    <RouterLink :to="{ name: 'cart' }" class="relative">
      <button
        class="bg-slate-900 text-white px-4 py-2 rounded-lg hover:text-slate-200 transition duration-300 flex items-center cursor-grab"
      >
        <span class="mr-2">Cart</span>
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13l-1 6m1-6l1 6m10-6l1 6m-1-6l-1 6m-9 6h10m-5-6V9"
          ></path>
        </svg>
      </button>
    </RouterLink>
  </div>
</template>
