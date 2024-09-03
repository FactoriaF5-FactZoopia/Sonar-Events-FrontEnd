<script setup>
import NavbarAdmin from "@/components/NavbarAdmin.vue";
import Tables from "@/components/Tables.vue";
import AddButton from "@/components/AddButton.vue";
</script>

<template>
  <NavbarAdmin></NavbarAdmin>
  <main>
    <div id="space"></div>
    <div id="addspace"><AddButton></AddButton></div>
    <div id="table">
      <Tables></Tables>
    </div>
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
