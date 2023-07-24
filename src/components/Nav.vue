<template>
<!-- <nav class="navbar navbar-expand-lg navbar-light bg-light ">
  <div class="container-fluid align-items-center">
    <a class="navbar-brand mt-2 mt-lg-0" href="/">
      <img src="../assets/img/logo.png" alt="Logo" width="30" height="24" class="img-fluid" style= "height: 50px;
  width: auto;">
    </a>
  
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarTogglerDemo02" aria-controls="navbarTogglerDemo02" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarTogglerDemo02">
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
</nav> -->

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid" style="justify-content: space-around">
    <a class="navbar-brand mt-2 mt-lg-0" href="/">
      <img src="../assets/img/logo.png" alt="Logo" class="img-fluid" style= "height: 50px;
      width: auto;">
    </a>

    <div class="dropdown">
      <a class="dropdown-toggle" type="button" id="dropdownMenuButton1"      data-bs-toggle="dropdown" aria-expanded="false">
        <img :src="avatar_url" alt="Logo" class="img-fluid avatar" style= "height: 50px; width: 50px;">
      </a>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
        <li class="m-2"><router-link to="/account" class="dropdown-item">Profile</router-link></li>
        <li class="m-2"><a class="dropdown-item" @click="signOut">Log out</a></li>
      </ul>
    </div>
  </div>
</nav>

</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { onMounted} from "vue";
import { useRouter } from "vue-router";
import { ref } from 'vue';


//constant to save a variable that will hold the use router method
const route = "/";
const avatar_url = ref(null);
const userStore = useUserStore();
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

async function getAvatar() {
  await userStore.fetchUser();
  avatar_url.value = userStore.profile.avatar_url;
}

onMounted(() => {
getAvatar();
});

</script>

<style>
.avatar {
  border-radius: 50%;
}
</style>
