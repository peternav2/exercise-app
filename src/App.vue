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

    function removeWorkout(index) {
      workouts.value.splice(index, 1);
    }

    return {
      newWorkout,
      addNewWorkout,
      workouts,
      removeWorkout,
    };
  },
};
</script>

<template>
  <Nav> </Nav>

  <div class="container">
    <form @submit.prevent="addNewWorkout">
      <label>New workout</label>
      <input v-model="newWorkout" name="newTodo" />
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
