<template>
    <!--<nav class="navbar">
    <ul @click="emit('openBurger')">-->
    <li @click="emit('openBurger')" class="log-out-welcome">
        <button class="hamburger" type="button">
            <span class="hamburger__line"></span>
            <span class="hamburger__middle"></span>
            <span class="icon-bar hamburger__line"></span>
        </button>
        <div class="row dropdown" :class="{ 'dropdown-after': menuOpen }">
            <router-link id="hamburger-wrap" class="nav-home" to="/">
                Home
            </router-link>
            <ul class="navList">
                <li>
                    <router-link id="hamburger-wrap" class="nav-home" to="/">Task Manager</router-link>
                </li>
                <li>
                    <router-link id="hamburger-wrap" class="nav-home" to="/account">Your Account</router-link>
                </li>
            </ul>
        </div>
    </li>
    <!--</ul>
    </nav>-->
</template>
<script setup>

const emit = defineEmits(["openBurger"]);
const props = defineProps(["menuOpen"]);
/*new Vue({
    el: '#app',
    : {
        menuOpen: false
    }
});*/
/*let menuOpen2 = menuOpen;

const openBurger = () => {
    menuOpen2 = !menuOpen2;
    console.log(menuOpen2)
}*/
</script>