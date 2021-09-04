<template>
  <div id="app">
  <Lich/>
  </div>
</template>

<script>
import Lich from "./components/Lich";
export default {
  name: 'App',
  components: {
    Lich
  },
  data() {
    return {

    }
  }

}
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
