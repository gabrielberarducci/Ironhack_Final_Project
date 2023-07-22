<template>
  <!-- <div class="container">
    <img class="d-flex justify-content-center" src="../assets/img/logo.png" alt="">
    <div class="d-flex justify-content-center">
      <form @submit.prevent="signIn">
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email address</label>
          <input class="form-control" aria-describedby="emailHelp" type="email" placeholder="example@gmail.com" id="email" v-model="email" required>
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label">Password</label>
          <input type="password" class="form-control" placeholder="**********" id="password" v-model="password"  required>
        </div>
        <button type="submit" class="btn btn-primary ">Submit</button>
        <p class="without-account">Dont have an account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p>
      </form>
    </div>
  </div> -->

  <!-- Section: Design Block -->
<section class="text-center">
  <!-- Background image -->
  <div class="p-5 bg-image" style="background-color: rgb(4, 20, 36); height: 400px;">
    <img src="../assets/img/logo.png" alt="Logo" class="d-inline-block align-text-top" style="width:20rem;">  
  </div>
  <!-- Background image -->

  <div class="card mx-4 mx-md-5 shadow-5-strong" style="
        margin-top: -30px;
        background: hsla(0, 0%, 100%, 0.8);
        backdrop-filter: blur(30px);
        ">
    <div class="card-body py-5 px-md-5">
      <div class="row d-flex justify-content-center">
        <div class="col-lg-8">

          <h2 class="fw-bold mb-5">Sign In</h2>
          <form @submit.prevent="signIn">
            <!-- 2 column grid layout with text inputs for the first and last names -->
            <!-- Email input -->
            <div class="form-outline mb-4">
              <input type="email" id="email" v-model="email" required class="form-control" placeholder="example@mail.com" />
              <label class="form-label" for="form3Example3">Email address</label>
            </div>

            <!-- Password input -->
            <div class="form-outline mb-4">
              <input type="password" placeholder="**********" id="password" v-model="password" required class="form-control" />
              <label class="form-label" for="form3Example4">Password</label>
            </div>

            <!-- Submit button -->
            <button type="submit" class="btn btn-primary btn-block mb-4">
              Sign In
            </button>
            <p class="without-account">Dont have an account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p>
         </form>
        </div>
      </div>
    </div>
  </div>
</section>
<!-- Section: Design Block -->
</template>

<script setup>
import PersonalRouter from "./PersonalRouter.vue";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { ref, reactive} from "vue"
// Route Variables
const route = "/auth/signup";
const buttonText = "Sign Up";


// variables para conectarme al form (login)

const email = ref("")
const password = ref("")

// Router to push user once SignedIn to Home
const redirect = useRouter();

// Arrow function to Signin user to supaBase

const signIn = async () => {
  try {
    // escribir comectario, tarea para casa.
    await useUserStore().signIn(email.value, password.value);
     // redirects user to the homeView
    redirect.push({ path: "/" });

  } catch (error) {
    alert(error)
  }
};
</script>

<style>
.without-account {
  padding-top: 1.5rem;
}
</style>
