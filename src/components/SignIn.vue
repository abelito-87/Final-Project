<!-- COMPONENTE BOILERPLATE -->
 
<template>
  
   <body>


    <div class="container">
      <h3 class="header-title">Log In to ToDo App</h3>
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
          </div>
          <button class="button-login" type="submit">Log In</button>
          <p class="account">
            Dont have an account?
            <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link" />
          </p>
        </div>
      </form>
      <img src="https://res.cloudinary.com/dn73thusg/image/upload/v1670485657/Final-Project/mesa_trabajo_ohzrvn.jpg"
        id="mesa-trabajo" alt="Mesa de trabajo con ordenadore y cafe">
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
</script>

<style>

</style>
