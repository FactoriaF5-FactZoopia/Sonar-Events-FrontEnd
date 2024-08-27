<script setup>
import { RouterLink, RouterView } from "vue-router";
import Navbar from "./components/Navbar.vue";

import Footer from "./components/Footer.vue";
</script>

<template>
  <header>
    <Navbar></Navbar>
  </header>

  <RouterView />
  <main></main>
  <Footer></Footer>
</template>

<style scoped></style>
