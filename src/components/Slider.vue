<script setup></script>

<template>
  <main>
    <div
      id="carouselExample"
      class="carousel slide"
      data-bs-ride="carousel"
      data-bs-interval="3000"
    >
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img src="../assets/img/music1.jpg" class="d-block w-100" alt="..." />
        </div>
        <div class="carousel-item">
          <img src="../assets/img/music2.jpg" class="d-block w-100" alt="..." />
        </div>
        <div class="carousel-item">
          <img src="../assets/img/music3.jpg" class="d-block w-100" alt="..." />
        </div>
      </div>
      <button
        class="carousel-control-prev"
        type="button"
        data-bs-target="#carouselExample"
        data-bs-slide="prev"
      >
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button
        class="carousel-control-next"
        type="button"
        data-bs-target="#carouselExample"
        data-bs-slide="next"
      >
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
    </div>
  </main>
</template>

<style scoped>
#carouselExample {
  width: 100%;
  height: 300px;
}

img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  object-position: bottom;
}
</style>
