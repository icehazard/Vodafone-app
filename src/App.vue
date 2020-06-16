<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from "./Views/Home.vue"

export default {
  name: "App",
  components: {
    Home
  }
};
</script>

<style>
.center {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.mb-70 {
  margin-bottom: 70px;
}

.mb-40{
  margin-bottom: 40px;
}
</style>

