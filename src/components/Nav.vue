<template>
  <div id="container-fluid">
    <nav class="navbar">
      <!-- <PersonalRouter :route="route" :buttonText="buttonText" class="logo-link"/> -->
      <!--  <router-link id="hamburger-wrap" class="nav-home" to="/">
        Home
      </router-link>
      <ul class="link-list">
        <li class="task-manager">
          <router-link id="hamburger-wrap" class="nav-home" to="/">Task Manager</router-link>
        </li>
        <li class="your-account">
          <router-link id="hamburger-wrap" class="nav-home" to="/account">Your Account</router-link>
        </li>
      </ul> -->
      <ul class="link-list">
        <burguer @openBurger="openBurger" :menuOpen="menuOpen" />
        <li>
          <p class="welcome">Welcome, user</p>
          <button @click="signOut" class="button-logout">Log out</button>
        </li>

      </ul>

    </nav>
  </div>

</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { computed } from "vue";
import { useRouter } from "vue-router";
import { ref } from 'vue';
import burguer from "./burguer.vue";

//import burguer from './burguer.vue'

//constant to save a variable that will hold the use router method
const route = "/";
const buttonText = "Todo app";

// funcion burguer

let menuOpen = ref(false);
const openBurger = () => {
  menuOpen.value = !menuOpen.value;
  console.log(menuOpen)
}

// constant to save a variable that will get the user from store with a computed function imported from vue
// const getUser = computed(() => useUserStore().user);
const getUser = useUserStore().user;

// constant that calls user email from the useUSerStore
const userEmail = getUser.email;

// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.

//DECLARAR VARIABLES

const redirect = useRouter();
const errorMsg = ref("error");

//CREAR FUNCIO ASYNC DEL SIGNOUT PER TORNAR A LA PAGINA INICI

const signOut = async () => {
  try {
    await useUserStore().signOut();
    console.log("meme");
    redirect.push({ path: "/auth/login" });
    // call the user store and send the users info to backend to signOut
    // then redirect user to the homeView
  } catch (error) {
    errorMsg.value = error.message;
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
  return;
  errorMsg.value = "error";
};

</script>

<style>

</style>
