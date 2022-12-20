<template>
  <v-app>
    <v-main class="bg">
      <HelloWorld />
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
<style>
.bg{
background-color: #FFFFFF;
color: black;
}

</style>
