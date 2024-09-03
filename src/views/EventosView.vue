<script setup>
import Navbar from "@/components/Navbar.vue";
import CardHome from "@/components/CardHome.vue";
</script>

<template>
  <Navbar></Navbar>
  <main>
    <div id="space"></div>
    <CardHome></CardHome>
    <div id="space"></div>
  </main>
</template>
<style scoped>
main {
  height: auto;
  background-color: #cca9f6;
}
#space {
  height: 100px;
}
</style>
