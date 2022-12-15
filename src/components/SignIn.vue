<!-- COMPONENTE BOILERPLATE -->
 
<template>

  <body>
    <div class="div-logo">
      <img id="logo"
        src="https://res.cloudinary.com/dn73thusg/image/upload/v1671006278/Final-Project/ToDo_App_kvnzp6.jpg"
        alt="logo ToDo App">
    </div>
    <div class="container">
      <h3 class="header-title"> Welcome to ToDo App </h3>
      <h5 class="header-subtitle-signin">Here you can create your to-do lists</h5>

      <!--<p class="header-subtitle">Estamos en la ruta de login. Aquí deberíais crear un form con la lógica correspondiente
        para que este permita al usuario loguearse con su email y su contraseña. Miraros la lógica de SignUp si
        necesitáis inspiración :)</p>
      <p>Dont have an account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p> -->
    </div>
    <!--COMENÇO A ESCRIURE------------------------------------->
    <div class="flex-Container">
      <form @submit.prevent="signIn" class="form-sign-in">
        <div class="form">
          <div class="form-input">
            <label class="input-field-label">E-mail</label>
            <input type="email" class="input-field" placeholder="example@gmail.com" id="email" v-model="email"
              required />
          </div>
          <div class="form-input">
            <label class="input-field-label">Password</label>
            <input type="password" class="input-field" placeholder="**********" id="password" v-model="password"
              required />
            <!--mostrar contrassenya-->
            <input class="show-password" type="button" name="wf" @click="mostrar()" value="Show password">
            <!---->
          </div>
          <button class="button-login" type="submit">Log In</button>
          <p class="account">
            Dont have an account?
            <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link" />
          </p>
        </div>
      </form>
      <div>
        <img src="https://res.cloudinary.com/dn73thusg/image/upload/v1670516350/Final-Project/img_signin_hzpcs0.jpg"
          id="image-zen" alt="imagen zen">
      </div>
    </div>
    <div v-show="errorMsg">{{ errorMsg }}</div>

    <!--AQUI ACABO--------------------------------------------->
  </body>
</template>


<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { ref, computed } from "vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";


// Route Variables
const route = "/auth/signup";
const buttonText = "Sign Up";
//const errorMsg = ref("Ha habido un error");
const errorMsg = ref("")

const redirect = useRouter();

// Arrow function to Signin user to supaBase

// AQUI ESCRIC JO
const signIn = async () => {
  try {
    await useUserStore().signIn(email.value, password.value);
    redirect.push({ path: "/" });
  } catch (error) {
    errorMsg.value = error.message;
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);

  }
  return;

  errorMsg.value = "error";
};
// AQUI ACABO

//mostrar contraseña



function mostrar() {
  let tipo = document.getElementById("password");

  if (tipo.type == "password") {
    tipo.type = 'text';
  } else {
    tipo.type = 'password';
  }

}


</script>

<style>

</style>
