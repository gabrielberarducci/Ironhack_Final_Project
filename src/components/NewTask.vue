<template>
    <button v-if="!newTaskBtn" @click="addToggle" class="button btn btn-warning  btn-block mt-4">
        Create New Task
    </button>     
    <div class="card m-4 p-3" v-if="newTaskBtn">
        <form>
            <h2 class="fw-bold m-4">Create New Task</h2>
            <input class="form-control mb-4" type="text" placeholder="Title" v-model="name"/>
            <textarea class="form-control mb-4" type="textarea" placeholder="Description" v-model="description"></textarea>
            <button @click="addTask" class="button btn btn-primary btn-block mb-4 me-4">Add</button>
            <button @click="addToggle" class="button btn btn-primary btn-block mb-4">Cancel</button> 
        </form>   
    </div>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task"   
import Swal from 'sweetalert2';

const taskStore = useTaskStore();

// variables para los valors de los inputs
const name = ref('');
const description = ref('');
const newTaskBtn = ref(false);


const addToggle = () => {
    newTaskBtn.value = !newTaskBtn.value;
};

// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const showErrorMessage = ref(false);

// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);

// Arrow function para crear tareas.
const addTask = async () => {
    if(name.value.length < 4 || description.value.length < 4){
        // Primero comprobamos que ningún campo del input esté vacío y lanzamos el error con un timeout para informar al user.

        showErrorMessage.value = true;
        errorMessage.value = 'Please write more than 3 caracters';
        Swal.fire({
        icon: 'error',
        title: 'Something Went Wrong!',
        text: 'Error: ' + errorMessage.value, 
      })
        setTimeout(() => {
            showErrorMessage.value = false;
        }, 5000);
    } else {
        // Aquí mandamos los valores a la store para crear la nueva Task. Esta parte de la función tenéis que refactorizarla para que funcione con emit y el addTask del store se llame desde Home.vue.

        taskStore.addTask(name.value, description.value);
        name.value = '';
        description.value = '';
        addToggle();
    }
};
</script>

<style></style>
  