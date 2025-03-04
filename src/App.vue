<script setup>
import { RouterView } from "vue-router";
import Navbar from "./components/Navbar.vue";
</script>

<template>
  <div class="min-h-screen flex flex-col bg-slate-300">
    <Navbar />
    <main class="flex-1 container mx-auto p-6">
      <RouterView />
    </main>
  </div>
</template>
