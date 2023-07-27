<template>
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
            <h2 class="fw-bold mb-5">Sign Up</h2>
            <form @submit.prevent="signUp">
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

              <!-- Confirm Password input -->
              <div class="form-outline mb-4">
                <input type="password" placeholder="**********" id="confirmPassword" v-model="confirmPassword" required class="form-control" />
                <label class="form-label" for="form3Example4">Confirm your Password</label>
              </div>

              <!-- Submit button -->
              <button type="submit" class="btn btn-primary btn-block mb-4">
                Sign Up
              </button>
              <p class="without-account">Already have an Account? <PersonalRouter :route="route" :buttonText="buttonText" class="sign-up-link"/></p>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import PersonalRouter from "./PersonalRouter.vue";
import { supabase } from "../supabase";
import { useRouter } from "vue-router";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
import Swal from 'sweetalert2';

// Route Variables
const route = "/auth/login";
const buttonText = "Sign In";

// Input Fields
const email = ref("");
const password = ref("");
const confirmPassword = ref("");

// Error Message
const errorMsg = ref("");

// Router to push user once SignedUp to Log In
const redirect = useRouter();

// Arrow function to SignUp user to supaBase with a timeOut() method for showing the error
const signUp = async () => {
  if (password.value === confirmPassword.value) {
    try {
      // calls the user store and send the users info to backend to logIn
      await useUserStore().signUp(email.value, password.value);
      Swal.fire({
        icon: 'success',
        title: 'Account Successfully Created', 
        text: 'Please confirm your E-amil',
        showConfirmButton: false,
        timer: 3000
      })
      // redirects user to the homeView
      redirect.push({ path: "/auth/login" });
    } catch (error) {
      // displays error message
      errorMsg.value = error.message;
      Swal.fire({
        icon: 'error',
        title: 'Something went Wrong!',
        text: 'Error: ' + errorMsg.value, 
      })
      // hides error message
      setTimeout(() => {
        errorMsg.value = null;
      }, 5000);
    }
    return;
  } else {
    errorMsg.value = 'error';
    Swal.fire({
      icon: 'error',
      title: 'Passwords are not the same',
      text: 'Please Try again...',
      showConfirmButton: false,
      timer: 2000
    })
  }
  errorMsg.value = "error";
};
</script>

<style></style>
