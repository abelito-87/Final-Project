<template>
  <nav>
    <!-- <PersonalRouter :route="route" :buttonText="buttonText" class="logo-link"/> -->
    <router-link class="nav-home" to="/">
      Home
    </router-link>

    <ul>
        <li>
          <router-link class="nav-home" to="/">Task Manager</router-link>
        </li>

        <li>
          <router-link class="nav-home" to="/account">Your Account</router-link>
        </li>
    </ul>

    <div>
      <ul>
        <li class="log-out-welcome">
          <p class="welcome">Welcome, user</p>
        </li>
        <li>
          <button @click="signOut" class="button-logout">Log out</button>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { computed } from "vue";
import { useRouter } from "vue-router";
import { ref } from 'vue';

//constant to save a variable that will hold the use router method
const route = "/";
const buttonText = "Todo app";

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
    redirect.push({path:"/auth/login"});
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
.navbar-img {
  width: 90px;
}

nav {
  /*background-color: #EBECEE;*/
  display: flex;
  width: 100%;
  justify-content: space-around;
  align-items: center;
}

nav ul {
  list-style: none;
  padding-inline-start: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
}

.nav-home {
  text-decoration: none;
  font-weight: bold;
  color: #c3bcbc;
  font-size: 1.2rem;
  padding: 30px 20px;
}

.button-logout {
    color: #fafafa;
    margin:  20px 20px 20px 0;;
    padding: 5px 20px;
    border: 0px solid;
    border-radius: 10px;
    background-color: #E94D4D;
}

.welcome {
  font-weight: bold;
  font-size: 1.2rem;
  margin-top: 20px;
}



</style>
