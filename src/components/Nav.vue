<template>
<nav class="navbar navbar-expand-lg">
  <div class="container-fluid" style="justify-content: space-around">
    <router-link to="/" class="navbar-brand mt-2 mt-lg-0">
      <img src="../assets/img/logo.png" alt="Logo" class="img-fluid" style= "height: 50px;
      width: auto;">
    </router-link>
    <div class="text-light"><p class="date">{{ fechaFormateada }}</p></div>
    <div class="dropdown">
      <a class="dropdown-toggle text-light" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
        <img :src="avatar_url" alt="Logo" class="img-fluid avatar" style="width: 50px; height: 50px; object-fit: cover;">
      </a>
      <ul class="dropdown-menu dropdown-menu-right dropdown-menu-dark" aria-labelledby="dropdownMenuButton1">
        <li class="p-0"><router-link to="/account" class="dropdown-item">Profile</router-link></li>
        <li class="p-0"><a class="dropdown-item" @click="signOut">Log out</a></li>
      </ul>
    </div>
  </div>
</nav>
</template>

<script setup>
// import PersonalRouter from "./PersonalRouter.vue";
import { useUserStore } from "../stores/user";
import { onMounted, watch} from "vue";
import { useRouter } from "vue-router";
import { ref } from 'vue';
import { format } from 'date-fns';


//constant to save a variable that will hold the use router method
const route = "/";
const avatar_url = ref(null);
const userStore = useUserStore();
const buttonText = "Todo app";
const fechaFormateada = ref('');

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

  // Obtener la fecha actual
  const fecha = new Date();

  // Formatear la fecha en el formato deseado (por ejemplo, "8th July 2023")
  const formatoFecha = format(fecha, "dd MMMM yyyy");

  // Asignar la fecha formateada a la variable fechaFormateada
  fechaFormateada.value = formatoFecha;

});

watch(
  () => userStore.profile,
  (updatedProfileData) => {
    avatar_url.value = updatedProfileData.avatar_url;
  },
  { deep: true }
);

</script>

<style>
.avatar {
  border-radius: 50%;
}

nav {
  background-color: rgb(4, 20, 36);
}

.date {
  font-size: 1.5rem;
  font-weight: 900;
  text-align: center;
}

.dropdown-menu {
  --bs-dropdown-min-width: 5rem;
}
</style>
