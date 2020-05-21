<template>
  <div id="app">
    <SirenHead/>
  </div>
</template>

<script>
import SirenHead from './components/SirenHead.vue'

export default {
  name: 'App',
  components: {
    SirenHead
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body, html {
  margin: 0;
  padding: 0;
}
</style>
