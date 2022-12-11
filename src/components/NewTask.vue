<template>
    <h1 class="add">Add a new Task</h1>
    <div v-if="showErrorMessage">
        <p class="error-text">{{ errorMessage }}</p>
    </div>
    <div>
        <div class="input-field-task">
            <input type="text" placeholder="Add a Task Title" v-model="name">
        </div>
        <div class="input-field-task-descript">
            <input type="text" placeholder="Add a Task Description" v-model="description">
        </div>
        <button @click="addTask" class="button-add">Add</button>
    </div>
    
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task"   




const taskStore = useTaskStore();

// variables para los valors de los inputs
const name = ref('');
const description = ref('');

// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const showErrorMessage = ref(false);

// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);

// Arrow function para crear tareas.
const addTask = () => {
if(name.value.length <= 3  || description.value.length === 0){
    // Primero comprobamos que ningún campo del input esté vacío y lanzamos el error con un timeout para informar al user.

    showErrorMessage.value = true;
    errorMessage.value = 'The task title or description is empty';
    setTimeout(() => {
    showErrorMessage.value = false;
    }, 5000);

} else {
    // Aquí mandamos los valores a la store para crear la nueva Task. Esta parte de la función tenéis que refactorizarla para que funcione con emit y el addTask del store se llame desde Home.vue.

    taskStore.addTask(name.value, description.value);
    name.value = '';
    description.value = '';

    
}
};

</script>

<style>

.add {
    text-align: center;
    font-weight: bold;
    font-size: 1.5rem;
    margin: 30px 0;
    font-family: 'Rock Salt', cursive;
}

.input-field-task {
    display: flex;
    flex-direction: column;
    padding: 0 25%;
    margin-bottom: 20px;
    
}

.input-field-task-descript {
    display: flex;
    flex-direction: column;
    padding: 0 25%;
    margin-bottom: 20px;
}

.button-add {
    color: #fafafa;
    margin:  20px 20px 20px 0;;
    padding: 5px 20px;
    border: 0px solid;
    border-radius: 10px;
    background-color: #E94D4D;
    display: flex;
    flex-direction: column;
    justify-content: center;
}
</style>
  