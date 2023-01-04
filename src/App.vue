<template>
  <div class="grid content-center p-5 justify-center">
    <img
      alt="Imagem com o rosto de Maurílio Atila"
      src="./assets/logo.png"
      class="w-52"
    />
    <Introduction msg="Maurilio Atila" />
  </div>
</template>

<script>
import Introduction from "./components/MyIntroduction.vue";

export default {
  name: "App",
  components: {
    Introduction,
  },
};
</script>
<style>
body {
  background: rgb(3, 128, 57);
  background-image: linear-gradient(to right, indigo, purple, orange);
}
</style>
