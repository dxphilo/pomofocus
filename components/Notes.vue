<template>
  <!-- Notes usage component-->
  <div class="notes">
    <h2 class="text-2xl text-center font-semibold py-2">Usage</h2>
    <div class="flex justify-center">
      <ol>
        <li class="text-xl py-1">Add task to be done</li>
        <li class="text-xl py-1">Double click to mark completed task</li>
        <li class="text-xl py-1">Click x to delete task</li>
      </ol>
    </div>
  </div>
</template>
<script>
export default {
  name: "Notes",
};
</script>
<style scoped>
ol {
  list-style: none;
  counter-reset: my-awesome-counter;
}
li {
  counter-increment: my-awesome-counter;
  margin: 0.25rem;
}
li::before {
  content: counter(my-awesome-counter);
  background: #662974;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  display: inline-block;
  line-height: 2rem;
  color: white;
  text-align: center;
  margin-right: 0.5rem;
}
ol ol li::before {
  background: #de51ff;
}
</style>