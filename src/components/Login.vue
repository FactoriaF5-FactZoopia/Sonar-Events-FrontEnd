<script>
import { usePopupStore } from '../stores/popup';

export default {
  name: 'LoginComponent',
  data() {
    return {
      isLoginActive: true,
      loginEmail: '',
      loginPassword: '',
      signupEmail: '',
      signupPassword: '',
      confirmPassword: ''
    }
  },
  methods: {
    setLoginActive(value) {
      this.isLoginActive = value;
    },
    handleLogin() {
      console.log('Login attempt', this.loginEmail, this.loginPassword);
    },
    handleSignup() {
      console.log('Signup attempt', this.signupEmail, this.signupPassword);
    },
    forgotPassword() {
      console.log('Forgot password');
    },
    
    toggleForm(form) {
      if (form === 'login') {
        this.isLogin = true;
        this.isSignup = false;
      } else {
        this.isLogin = false;
        this.isSignup = true;
      }
    },
    submitForm(form) {
      if (form === 'login') {
        console.log('Login:', this.loginEmail, this.loginPassword);
        this.closePopup();
      } else {
        console.log('Signup:', this.signupEmail, this.signupPassword, this.confirmPassword);
        this.closePopup();
      }
    },
    closePopup() {
      const popupStore = usePopupStore();
      popupStore.closePopups();
    }
  },
  setup() {
    const popupStore = usePopupStore();
    return { popupStore };
  }
};

</script>
<template>
      <div v-if="popupStore.isLoginOpen" class="popup-overlay" @click.self="closePopup">

  <div class="wrapper">
    <div class="title-text">
      <div class="title login" :class="{ active: isLoginActive }">Login Form</div>
      <div class="title signup" :class="{ active: !isLoginActive }">Signup Form</div>
    </div>
    <div class="form-container">
      <div class="slide-controls">
        <input type="radio" name="slide" id="login" v-model="isLoginActive" :value="true">
        <input type="radio" name="slide" id="signup" v-model="isLoginActive" :value="false">
        <label for="login" class="slide login" @click="setLoginActive(true)">Login</label>
        <label for="signup" class="slide signup" @click="setLoginActive(false)">Signup</label>
        <div class="slider-tab" :style="{ left: isLoginActive ? '0%' : '50%' }"></div>
      </div>
      <div class="form-inner">
        <form @submit.prevent="handleLogin" v-if="isLoginActive">
          <div class="field">
            <input type="text" v-model="loginEmail" placeholder="Email Address" required>
          </div>
          <div class="field">
            <input type="password" v-model="loginPassword" placeholder="Password" required>
          </div>
          <div class="field btn">
            <div class="btn-layer"></div>
            <input type="submit" value="Login">
          </div>
        </form>
        <form @submit.prevent="handleSignup" v-else>
          <div class="field">
            <input type="text" v-model="signupEmail" placeholder="Email Address" required>
          </div>
          <div class="field">
            <input type="password" v-model="signupPassword" placeholder="Password" required>
          </div>
          <div class="field">
            <input type="password" v-model="confirmPassword" placeholder="Confirm password" required>
          </div>
          <div class="field btn">
            <div class="btn-layer"></div>
            <input type="submit" value="Signup">
          </div>
        </form>
      </div> 
    </div> 
    </div>
  </div>
</template>



<style scoped>
 @import url("https://fonts.googleapis.com/css?family=Poppins:400,500,600,700&display=swap");
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;
  }
  html,
  body {
    display: grid;
    height: 100%;
    width: 100%;
    place-items: center;
    background: #282a36;
  }
  ::selection {
    background: #1a75ff;
    color: #fff;
  }
  .wrapper {
    overflow: hidden;
    max-width: 390px;
    background: #301f35;
    padding: 30px;
    border-radius: 15px;
    box-shadow: 0px 15px 20px rgba(0, 0, 0, 0.1);
    border: solid 3px rgb(212, 48, 137);
  }
  .wrapper .title-text {
    display: flex;
    width: 200%;
  }
  .wrapper .title {
    color: rgb(212, 48, 137);
    width: 50%;
    font-size: 35px;
    font-weight: 600;
    text-align: center;
    transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  }
  .wrapper .slide-controls {
  position: relative;
  display: flex;
  height: 50px;
  width: 100%;
  overflow: hidden;
  margin: 30px 0 10px 0;
  justify-content: space-between;
  border: 1px solid rgb(212, 48, 137);
  border-radius: 15px;
}
  
.slide-controls .slide {
  height: 100%;
    width: 100%;
    color: #fff;
    font-size: 18px;
    font-weight: 500;
    text-align: center;
    line-height: 48px;
    cursor: pointer;
    z-index: 1;
    transition: all 0.6s ease;
}

  .slide-controls label.signup {
    color: white;
  }
  .slide-controls .slider-tab {
  position: absolute;
  height: 100%;
  width: 50%;
  left: 0;
  z-index: 0;
  border-radius: 15px;
  background: -webkit-linear-gradient(left, #430745, #680d6c, #9a0c9f, #c212c8);
  transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
#signup:checked ~ .slider-tab {
  left: 50%;
}

  input[type="radio"] {
    display: none;
  }
  .move-right {
    left: 50%;
  }
  .wrapper .form-container {
    width: 100%;
    overflow: hidden;
  }
  .form-container .form-inner {
    display: flex;
    width: 200%;
  }
  .form-container .form-inner form {
    width: 50%;
    transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  }
  .form-inner form .field {
    height: 50px;
    width: 100%;
    margin-top: 20px;
  }
  .form-inner form .field input {
    height: 100%;
    width: 100%;
    outline: none;
    padding-left: 15px;
    border-radius: 15px;
    border: 1px solid lightgrey;
    border-bottom-width: 2px;
    font-size: 17px;
    transition: all 0.3s ease;
  }
  .form-inner form .field input:focus {
    border-color: #1a75ff;
  }
  .form-inner form .field input::placeholder {
    color: #999;
    transition: all 0.3s ease;
  }
  form .field input:focus::placeholder {
    color: #1a75ff;
  }
  .form-inner form .pass-link {
    margin-top: 5px;
  }
  .form-inner form .signup-link {
    text-align: center;
    margin-top: 30px;
  }
  .form-inner form .pass-link a,
  .form-inner form .signup-link a {
    color: #1a75ff;
    text-decoration: none;
  }
  .form-inner form .pass-link a:hover,
  .form-inner form .signup-link a:hover {
    text-decoration: underline;
  }
  form .btn {
    height: 50px;
    width: 100%;
    border-radius: 15px;
    position: relative;
    overflow: hidden;
  }
  form .btn .btn-layer {
    height: 100%;
    width: 300%;
    position: absolute;
    left: -100%;
    background: -webkit-linear-gradient(
      right,
      #c212c8,
      #c310c9,
      #590b5c,
      #1f0320
    );
    border-radius: 15px;
    transition: all 0.4s ease;
  }
  form .btn:hover .btn-layer {
    left: 0;
  }
  form .btn input[type="submit"] {
    height: 100%;
    width: 100%;
    z-index: 1;
    position: relative;
    background: none;
    border: none;
    color: #fff;
    padding-left: 0;
    border-radius: 15px;
    font-size: 20px;
    font-weight: 500;
    cursor: pointer;
  }
  #signup:checked ~ .slider-tab {
  left: 50%;
}

#signup:checked ~ label.signup {
  color: #fff;
  cursor: default;
  user-select: none;
}

#signup:checked ~ label.login {
  color: white;
}

#login:checked ~ label.signup {
  color: white;
}

#login:checked ~ label.login {
  cursor: default;
  user-select: none;
}

/* Agregar estas clases para la animación de fade */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.popup-overlay {
  position: fixed;
  top: 125px;
  margin-right: 10px;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  justify-content: center;
  align-items: center;
  z-index: 1000;
  display: flex;
  justify-content: flex-end; 
  align-items: flex-start; 
 
}
</style>