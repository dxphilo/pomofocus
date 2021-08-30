<template>
  <!-- PomoFocus Timer Componenent -->
  <div>
    <div class="timer">
      <!-- start of the tabs section-->
      <div class="text-center flex justify-center pb-0 mb-0 mt-4 h-16">
        <div>
          <div class="tabs">
            <button
              class="
                text-lg
                ml-3
                bg-purple-200
                hover:bg-purple-300
                rounded
                py-1.5
                px-5
              "
              @click="toggle"
            >
              Pomodoro
            </button>
            <button
              class="
                text-lg
                ml-3
                bg-purple-200
                hover:bg-purple-300
                rounded
                py-1.5
                px-5
              "
              @click="toggle"
            >
              Short Break
            </button>
          </div>
        </div>
      </div>
      <!-- end of the tabs section -->
      <!-- start of the timer section -->

      <div class="timers">
        <!-- show full time when Pomodoro is clicked -->
        <div v-if="tabs">
          <Timer />
        </div>
        <!-- other wise show short break when short break button is clicked -->
        <div v-else>
          <Shortbreak />
        </div>
      </div>

      <!-- end of the timer section -->
    </div>

    <!-- TASKS SECTION -->
    <div class="tasks">
      <h2 class="pt-8 text-2xl py-6">Tasks:</h2>
      <div class="w-1/4 my-0 mx-auto">
        <hr class="py-4" />
      </div>
      <div v-for="task in tasks" :key="task.title" id="task.title">
        <Task v-bind:task="task" v-on:deleteTask="deleteTask" />
      </div>
      <div class="addtask">
        <form @submit.prevent="updateTasks">
          <input
            type="text"
            class="
              py-3
              rounded
              w-96
              px-8
              bg-purple-600
              hover:bg-purple-800
              text-white text-xl
              mb-2
              border-l-4
              outline-none
              text-center
            "
            name="task"
            id="task"
            v-model="addtask"
            placeholder="Add tasks here ..."
          />
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import Shortbreak from "./Shortbreak.vue";
const notificationSound = require("@/assets/goeswithoutsaying.mp3").default;
export default {
  name: "Home",
  components: {
    Shortbreak,
  },
  data() {
    return {
      isActive: false,
      tasks: [
        {
          title: "edit youtube video",
          edit: false,
          complete: false,
        },
        {
          title: "write a blog post",
          edit: false,
          complete: false,
        },
      ],
      tabs: true,
      addtask: "",
    };
  },
  methods: {
    // update the tasks
    updateTasks() {
      if (this.addtask === "") {
        alert("Please enter task to proceed");
      } else {
        let newTask = {
          title: this.addtask,
          complete: false,
          edit: false,
        };
        this.tasks.push(newTask);
        this.addtask = "";
        console.log("Task has been updated successfully");
      }
    },
    // delete the task
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.title !== id);
    },
    // toggle between work and long breaks
    toggle() {
      this.tabs = !this.tabs;
    },
  },
};
</script>
<style scoped>
</style>