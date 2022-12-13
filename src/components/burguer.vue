<template>
    <ul>
        <li class="log-out-welcome">
            <button class="hamburger" type="button">
                <span class="hamburger__line"></span>
                <span class="hamburger__middle"></span>
                <span class="icon-bar hamburger__line"></span>
            </button>
            <div class="row dropdown" :class="{ 'dropdown-after': menuOpen }">
                <router-link id="hamburger-wrap" class="nav-home" to="/">
                    Home
                </router-link>
                <ul class="link-list">
                    <li class="task-manager">
                        <router-link id="hamburger-wrap" class="nav-home" to="/">Task Manager</router-link>
                    </li>
                    <li class="your-account">
                        <router-link id="hamburger-wrap" class="nav-home" to="/account">Your Account</router-link>
                    </li>
                </ul>
            </div>
            <p class="welcome">Welcome, user</p>
        </li>
    </ul>
</template>
<script setup>
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