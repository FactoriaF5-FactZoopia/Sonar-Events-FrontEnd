<script setup></script>
<template>
  <footer class="text-center text-lg-start" style="background-color: #301f35">
    <div class="container d-flex justify-content-center py-5">
      <button
        type="button"
        class="btn btn-primary btn-lg btn-floating mx-2"
        id="btnfb"
      >
        <i class="fab fa-facebook-f"></i>
      </button>
      <button
        type="button"
        class="btn btn-primary btn-lg btn-floating mx-2"
        id="btntw"
      >
        <i class="fab fa-twitter"></i>
      </button>
      <button
        type="button"
        class="btn btn-primary btn-lg btn-floating mx-2"
        id="btnig"
      >
        <i class="fab fa-instagram"></i>
      </button>
      <button
        type="button"
        class="btn btn-primary btn-lg btn-floating mx-2"
        id="btnws"
      >
        <i class="fab fa-whatsapp"></i>
      </button>
    </div>

    <!-- Copyright -->
    <div
      class="text-center p-3"
      style="background-color: #404040"
      id="divfooter"
    >
      © 2024 Copyright:
      <a
        class="linkProyecto"
        href="https://github.com/FactoriaF5-FactZoopia/Sonar-Events-FrontEnd.git"
        target="_blank"
        >SonarEvents</a
      >
    </div>
    <!-- Copyright -->
  </footer>
</template>
<style scoped>
footer {
  box-shadow: 0 -10px 15px#d43089;
}
button {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  border: 2px solid white;
  background-color: #404040;
}

#btnfb:hover {
  transform: scale(1.1);
  background-color: #404040;
  box-shadow: 0 0 15px#3b5998;
  border: 2px solid #3b5998;
  color: #3b5998;
  transform: rotateY(360deg);
}

#btntw:hover {
  transform: scale(1.1);
  background-color: #404040;
  box-shadow: 0 0 15px#00acee;
  border: 2px solid #00acee;
  color: #00acee;
  transform: rotateY(360deg);
}
#btnig:hover {
  transform: scale(1.1);
  background-color: #404040;
  box-shadow: 0 0 15px#D43089;
  border: 2px solid #d43089;
  color: #d43089;
  transform: rotateY(360deg);
}
#btnws:hover {
  transform: scale(1.1);
  background-color: #404040;
  box-shadow: 0 0 15px#25D366;
  border: 2px solid #25d366;
  color: #25d366;
  transform: rotateY(360deg);
}
#btnws,
#btnig,
#btntw,
#btnfb {
  transition: transform 3s;
  transform-style: preserve-3d;
}
#divfooter {
  color: white;
  box-shadow: 0 0 15px#d43089;
}
.linkProyecto {
  font-size: 18px;
  color: #d43089;
}
@media (max-width: 600px) {
  button {
    width: 60px;
    height: 60px;
  }
}
</style>
