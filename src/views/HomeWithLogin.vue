<script setup>
import Slider from "@/components/Slider.vue";
import Toggle from "@/components/Toggle.vue";
import CardHome from "@/components/CardHome.vue";
import Login from "@/components/Login.vue";
import Navbar from "@/components/Navbar.vue";
</script>

<template>
  <Navbar></Navbar>
  <div id="blankspace"></div>
  <main>
    <div id="containerslider">
      <div id="slider">
        <Slider></Slider>
      </div>
    </div>
    <div id="containerToogle">
      <div id="toggle">
        <Toggle></Toggle>
      </div>
    </div>
    <div id="containerSpan">
      <div id="span">
        <span class="ms-3 text-sm font-medium text-gray-900 dark:text-gray-300"
          >Choose Past Events</span
        >
      </div>
    </div>
    <!--     <div class="bubbles">
      <span style="--i: 11"></span>
      <span style="--i: 12"></span>
      <span style="--i: 24"></span>
      <span style="--i: 10"></span>
      <span style="--i: 14"></span>
      <span style="--i: 23"></span>
      <span style="--i: 18"></span>
      <span style="--i: 16"></span>
      <span style="--i: 19"></span>
      <span style="--i: 20"></span>
      <span style="--i: 22"></span>
      <span style="--i: 25"></span>
      <span style="--i: 18"></span>
      <span style="--i: 21"></span>
      <span style="--i: 15"></span>
      <span style="--i: 13"></span>
      <span style="--i: 26"></span>
      <span style="--i: 17"></span>
      <span style="--i: 13"></span>
      <span style="--i: 28"></span>
    </div> -->
    <CardHome></CardHome>
    <div id="space"></div>
  </main>
  <div id="blankspace"></div>
</template>

<style scoped>
main {
  position: relative;
  width: 100%;
  background-color: #cca9f6;
  opacity: 1;
  height: auto;
  overflow: hidden;
}
#blankspace {
  height: 20px;
  background-color: #cca9f6;
}
.bubbles {
  position: relative;
  display: flex;
}

.bubbles span {
  position: relative;
  width: 30px;
  height: 30px;
  background: #4ad1f2;
  margin: 35px;
  border-radius: 50%;
  box-shadow: 0 0 0 0px white, 0 0 0px white, 0 0 0px white;
  animation: animate 50s linear infinite;
  animation-duration: calc(225s / var(--i));
}
.bubbles span:nth-child(even) {
  background: white;
  box-shadow: 0 0 0 0px #f0eded, 0 0 0px white, 0 0 0px white;
}

#containerslider {
  width: 100%;
  height: 370px;
  display: flex;
  justify-content: center;
  align-items: center;
}
#slider {
  width: 60%;
  height: 300px;
  background-color: white;

  box-shadow: 0 0 15px 15px #301f35;
}
#containerToogle {
  width: 100%;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}
#containerSpan {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
span {
  width: 70%;
  height: 25px;
  color: #301f35;
}

#space {
  height: 100px;
}

@keyframes animate {
  0% {
    transform: translateY(800px) scale(0);
  }
  100% {
    transform: translateY(1px) scale(1);
  }
}
@media (max-width: 768px) {
  #containerslider {
    display: none;
  }
}
</style>
