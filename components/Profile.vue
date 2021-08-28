<template>
  <!-- profile section component -->
  <div>
    <div>
      <img
        :src="$auth.user.picture"
        class="h-8 w-8 rounded inline border-2 border-purple-500"
      />
      <h2 class="inline">{{ $auth.user.given_name }}</h2>
    </div>
  </div>
</template>
<script>
export default {
  name: "Profile",
};
</script>
<style scoped>
</style>