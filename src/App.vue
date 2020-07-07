<template>
  <div id="app">
    <ChartContainer />
  </div>
</template>

<script>
import ChartContainer from './components/ChartContainer.vue'

export default {
  name: 'App',
  components: {
    ChartContainer
  }
}
</script>

<style lang="scss">
html, body {
background-color: #050711;
font-family: 'Montserrat', sans-serif;
}

#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
