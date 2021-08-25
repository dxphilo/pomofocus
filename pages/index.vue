<template>
  <div class="home bg-purple-400 w-full h-screen">
    <!-- start of the header component -->
    <div class="pomofocus flex justify-around py-4 text-xl">
      <div>
        <H1>PomoFocus</H1>
      </div>
      <div>
        <ul class="flex">
          <li><nuxt-link to="/about" class="pr-4">About</nuxt-link></li>
          <li>
            <div>
              <div v-if="!this.isLogged">
                <button type="button" @click="loginClick()">Login</button>
              </div>
              <div v-else>
                <button @click="logOut()">LogOut</button>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- end of the header -->
    <!--pomofocus component-->
    <div class="text-center py-10">
      <PomofocusTimer />
    </div>
  </div>
</template>
<script>
export default {
  name: "Home",
  components: {},
  data: () => {
    return {
      isLogged: "",
    };
  },
  methods: {},
};
</script>
<style scoped>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: calc(10px + 0.35vw);
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  scroll-behavior: smooth;
}
html:focus-within {
  scroll-behavior: smooth;
}
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
</style>
