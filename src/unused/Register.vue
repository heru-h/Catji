<template>
  <div class="register">
    <NavBar />
    <Registerr style="background-color: #f0f0f0;"></Registerr>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from "@/components/NavBar.vue";
import Registerr from "@/components/Registerr.vue";
export default {
  name: "Register",
  components: {
    Registerr,
    NavBar,
  },
};
</script>
