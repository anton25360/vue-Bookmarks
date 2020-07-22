<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Card name='amazon prime'/>
    <Card name='amazon prime22a'/>
    <Card name='amazon prime3'/>
    <Card name='amazon prime4'/>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    Card
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
