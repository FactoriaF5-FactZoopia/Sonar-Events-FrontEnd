<script setup>
import { RouterLink, RouterView } from "vue-router";
import NavbarSinLogin from "./components/NavbarSinLogin.vue"
import Footer from "./components/Footer.vue";

</script>

<template>
  <header>
    <!-- <Navbar></Navbar> -->
    <NavbarSinLogin></NavbarSinLogin>
    logub
  </header>

  <RouterView />
  <main></main>
  <Footer></Footer>
</template>

<style scoped></style>
