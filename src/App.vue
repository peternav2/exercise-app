<!-- eslint-disable vue/no-export-in-script-setup -->
<script>
import Nav from "./components/Nav.vue";
import { ref } from "vue";

export default {
  setup() {
    const newWorkout = ref("");

    const workouts = ref([]);

    function addNewWorkout() {
      workouts.value.push({
        id: Date.now(),
        done: false,
        content: newWorkout.value,
      });
      newWorkout.value = "";
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function markAllDone() {
      workouts.value.forEach((todo) => {
        todo.done = true;
      });
    }

    function removeWorkout(index) {
      workouts.value.splice(index, 1);
    }

    return {
      newWorkout,
      addNewWorkout,
      workouts,
      toggleDone,
      removeWorkout,
      markAllDone,
    };
  },
};
</script>

<template>
  <div class="container">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://bulma.io">
          <img src="src\assets\logo.jfif" width="75" height="max" />
        </a>
      </div>

      <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item"> Home </a>

          <a class="navbar-item"> Documentation </a>

          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link"> More </a>

            <div class="navbar-dropdown">
              <a class="navbar-item"> About </a>
              <a class="navbar-item"> Jobs </a>
              <a class="navbar-item"> Contact </a>
              <hr class="navbar-divider" />
              <a class="navbar-item"> Report an issue </a>
            </div>
          </div>
        </div>
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-primary">
                <strong>Sign up</strong>
              </a>
              <a class="button is-light"> Log in </a>
            </div>
          </div>
        </div>
      </div>
    </nav>
  </div>

  <div class="container">
    <form @submit.prevent="addNewWorkout">
    <label>New Todo</label>
    <input v-model="newWorkout" name="newTodo">
    <button class="button">Add</button>
  </form>
  </div>
  
  <hr />

  <ol>
    <li v-for="(workout, index) in workouts" :key="workout.id">
      <h3>
        {{ workout.content }}
      </h3>
      <button @click="removeWorkout(index)">Remove</button>
    </li>
  </ol>
</template>
