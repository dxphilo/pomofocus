<template>
  <!-- TASKS SECTION -->
  <div>
    <li
      class="
        py-3
        rounded
        w-96
        px-8
        bg-purple-700
        hover:bg-purple-800
        text-white text-xl
        mb-2
        border-l-4
        list-none
        my-0
        mx-auto
        focus:outline-none
      "
    >
      <h3
        class="inline focus:outline-none"
        v-bind:class="{ 'line-through': task.complete }"
        v-on:dblclick="isCompleted"
      >
        {{ task.title }}
      </h3>
      <button
        class="pl-8 text-red-500"
        @click="$emit('deleteTask', task.title)"
      >
        X
      </button>
    </li>
  </div>
</template>
<script>
export default {
  name: "Task",
  props: ["task"],
  data() {
    return {};
  },
  methods: {
    // isCompleted task
    isCompleted() {
      this.task.complete = !this.task.complete;
    },
  },
};
</script>
<style scoped>
</style>