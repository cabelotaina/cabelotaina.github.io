<template>
  <div
    class="grid content-center p-5 justify-center bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 h-screen"
  >
    <div class="flex items-center justify-center">
      <img alt="Imagem com o rosto de Maurílio Atila" src="./assets/logo.png" />
    </div>
    <HelloWorld msg="Hello! I'm Mau o/" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>
