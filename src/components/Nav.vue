<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light justify-content-center">
  <div class="nav justify-content-center align-items-center">
    <a class="navbar-brand mt-2 mt-lg-0" href="/">
      <img src="../assets/img/logo.png" alt="Logo" height="120" class="d-inline-block align-text-top">
    </a>
  
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav nav-underline">
        <li class="nav-item">
          <router-link to="/" class="nav-link" aria-current="page">Tasks</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/account" class="nav-link">Your Account</router-link>
        </li>
      </ul>

    </div>
    <button class="button btn btn-primary ms-3" style="height: 3rem;" @click="signOut">Log out</button>
  </div>
</nav>

</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { computed, onMounted} from "vue";
import { useRouter } from "vue-router";
import { ref } from 'vue';
import Profile from "../components/Profile.vue";

//constant to save a variable that will hold the use router method
const route = "/";
const avatar_url = ref(null);

const buttonText = "Todo app";

// constant to save a variable that will get the user from store with a computed function imported from vue

// const getUser = computed(() => useUserStore().user);
const getUser = useUserStore().user;

// constant that calls user email from the useUSerStore
const userEmail = getUser.email;

// async function that calls the signOut method from the useUserStore and pushes the user back to the Auth view.
const redirect = useRouter();

const signOut = async () => {
  try{

    await useUserStore().signOut();
    redirect.push({ path: "/auth/login" });
  
    // call the user store and send the users info to backend to signOut
    // then redirect user to the homeView
  } catch (error) {}
};
</script>

<style>
/* .navbar-img {
  width: 90px;
}

nav {
  background-color: lightgray;
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
} */
</style>
