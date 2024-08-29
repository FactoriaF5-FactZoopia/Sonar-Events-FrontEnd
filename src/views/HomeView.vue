<script setup>
import Login from "/src/components/Login.vue"
</script>

<template>
   <Login></Login>
  <main>
   
    <div class="bubbles">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
  </main>
</template>

<style scoped>
main {
  position: relative;
  width: 100%;

  background-color: blueviolet;
  opacity: 0.5;
  height: 800px;
  overflow: hidden;
}
.bubbles {
  position: relative;
  display: flex;
}

.bubbles span {
  position: relative;
  width: 30px;
  height: 30px;
  background: #00acee;
  margin: 0 4px;
  border-radius: 50%;
  box-shadow: 0 0 0 10px #00acee44, 0 0 50px #00acee, 0 0 100px #00acee;
  animation: animate 6s linear infinite;
}
.bubbles span:nth-child(even) {
  background: white;
  box-shadow: 0 0 0 10px #ff2d7544, 0 0 50px white, 0 0 100px white;
}

@keyframes animate {
  0% {
    transform: translateY(100vh) scale(0);
  }
  100% {
    transform: translateY(-10vh) scale(1);
  }
}
</style>
