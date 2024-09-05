<script setup>
import { ref } from "vue";
import { usePopupStore } from "../stores/popup";

const isMenuOpen = ref(false);
const popupStore = usePopupStore();

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const openLoginPopup = () => {
  popupStore.openLogin();
};
</script>

<template>
  <div class="flex flex-wrap h-screen" id="nav">
    <section class="relative mx-auto" id="mainnav">
      <nav class="flex justify-between bg-[#301f35] text-white w-screen">
        <div class="px-5 xl:px-12 py-6 flex w-full items-center">
          <img src="../assets//img/logosonar.png" id="logo" alt="" />
          <a
            class="text-3xl font-bold font-heading text-[white]"
            href="#"
            id="titulo"
            style="color: #d43089"
          >
            SonarEvents
          </a>

          <ul
            :class="`${
              isMenuOpen ? 'block' : 'hidden'
            } md:flex px-4 mx-auto font-semibold font-heading space-x-10`"
          >
            <RouterLink to="/">
              <li></li>
            </RouterLink>
            <RouterLink to="/eventos">
              <li></li>
            </RouterLink>
          </ul>

          <div class="hidden xl:flex items-center space-x-5 items-center">
            <div class="flex items-center hover:text-gray-200">
              <a
                class="hover:text-gray-200 font-semibold"
                id="logout"
                href="#"
                @click.prevent="openLoginPopup"
              >
                Log in
              </a>
              <img
                id="imgLogout"
                src="../assets/img/usuariosonar2.png"
                alt=""
                @click="openLoginPopup"
                class="cursor-pointer"
              />
            </div>
          </div>
        </div>

        <a
          class="navbar-burger self-center mr-12 xl:hidden"
          href="#"
          @click="toggleMenu"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6 hover:text-gray-200"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h16"
            />
          </svg>
        </a>
      </nav>
    </section>
  </div>
</template>

<style scoped>
#nav {
  height: auto;
}
#mainnav {
  box-shadow: 0 17px 20px#d43089;
  height: 120px;
}
#logo {
  width: 100px;
  filter: drop-shadow(0px 2px 8px #d43089);
  animation: rotar 5s linear infinite;
  display: flex;
  align-items: center;
}
@keyframes rotar {
  from {
    transform: rotateX(180deg);
  }
  to {
    transform: rotateX(-180deg);
  }
}
#titulo {
  font-size: 40px;
  display: flex;
  align-items: center;
}

#imgLogout {
  width: 50px;
}
#logout {
  margin-right: 20px;
}
#idHome,
#idEventos,
#logout {
  font-size: 25px;
  position: relative;
  padding: 6px;
  overflow: hidden;
}

#idHome:hover,
#idEventos:hover {
  color: #d43089;

  box-shadow: 0 5px 0 0 #d43089 inset, 0 5px 0 0 transparent;
}

#logout:hover {
  color: #d43089;
}

#idHome:hover::after,
#idEventos:hover::after {
  content: "";
  position: absolute;
  bottom: -5px;
  left: 0;
  height: 5px;
  width: 100%;
  background-color: #d43089;
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.35s ease;
  z-index: 1;
}

#idHome:hover::after,
#idEventos:hover::after {
  transform: scaleX(1);
}
@media (max-width: 600px) {
  #titulo {
    font-size: 15px;
  }
}
</style>
