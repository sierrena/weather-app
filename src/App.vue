<template>
  <div class="d-flex justify-content-center" id="app">
    <CameraSnap @picture-taken="imageSrc = $event" />
    <UserForm />
    <img :src="imageSrc" />
  </div>
</template>

<script>
import CameraSnap from "./components/CameraSnap.vue";
import UserForm from "./components/UserForm.vue";

export default {
  name: "App",
  components: {
    CameraSnap,
    UserForm,
  },
  data() {
    return {
      imageSrc: null,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
