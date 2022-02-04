<template>

  <Card />
  <Buttons />
</template>

<script>
import Card from "./components/Card.vue";
export default {
  name: "App",
  components: {
    Card,
  },
};
</script>

<style>
@import "./assets/css/bootstrap.min.css";
@import "./assets/css/main.css";

</style>
