<template>
  <!-- PomoFocus Timer Componenent -->
  <div>
    <div class="timer">
      <div class="text-center flex justify-center pb-0 mb-0 mt-4 h-16">
        <div v-for="tab in tabs" :key="tab">
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
            >
              {{ tab }}
            </button>
          </div>
        </div>
      </div>
      <div>
        <h4 class="text-9xl pt-0 mt-0 font-bold">
          {{ timerMinutes }}:{{ timerSeconds }}
        </h4>
        <div class="button-toggle">
          <button
            class="
              text-4xl
              mt-4
              rounded
              font-bold
              px-14
              py-3
              shadow-lg
              bg-purple-600
              hover:shadow-xl
              hover:bg-purple-700
            "
            @click="start"
            v-if="isActive === false"
          >
            START
          </button>
          <button
            class="
              text-4xl
              mt-4
              rounded
              font-bold
              px-14
              py-3
              shadow-lg
              bg-purple-600
              hover:shadow-xl
              hover:bg-purple-700
            "
            @click="stop"
            v-if="isActive === true"
          >
            STOP
          </button>
        </div>
      </div>
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
const notificationSound = require("@/assets/goeswithoutsaying.mp3").default;
export default {
  name: "Home",
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
      tabs: ["Pomodoro", "Short Break"],
      addtask: "",
      timerType: 0,
      totalSeconds: 1 * 60,
      shortbreak: "5:00",
      pomodoroInstance: null,
      notificationSound,
    };
  },
  computed: {
    // show minutes
    timerMinutes() {
      const minutes = Math.floor(this.totalSeconds / 60);
      return this.formatTime(minutes);
    },
    // show seconds
    timerSeconds() {
      let sec = this.totalSeconds % 60;

      return this.formatTime(sec);
    },
  },
  methods: {
    // formats time function
    formatTime(time) {
      if (time < 10) {
        return "0" + time;
      }
      return time.toString();
    },
    // start the timeer count
    start() {
      this.pomodoroInstance = setInterval(() => {
        this.totalSeconds -= 1;
        if (
          Math.floor(this.totalSeconds / 60) === 0 &&
          this.totalSeconds % 60 === 0
        ) {
          var audio = new Audio(this.notificationSound);
          audio.play();
          clearInterval(this.pomodoroInstance);
          (this.totalSeconds = 25 * 60), (this.isActive = false);
          console.log(audio);
        }
      }, 1000);
      this.isActive = true;
    },
    // stop the timer interval
    stop() {
      clearInterval(this.pomodoroInstance);
      this.isActive = false;
    },
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
  },
};
</script>
<style scoped>
</style>