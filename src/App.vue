<template>
  <div id="app">
    <Bar/>
    <img alt="Vue logo" src="./assets/logo.png">
    <Card name='Netflix'/>
    <Card name='Prime Video'/>
    <Card name='PLEX'/>
    <Card name='Quibi'/>
  </div>
</template>

<script>
import Card from './components/Card.vue'
import Bar from './components/Bar.vue'

export default {
  name: 'App',
  components: {
    Card,
    Bar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  border: 6px solid red;
  padding: 0;
  margin: 0;
}
</style>
