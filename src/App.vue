<template>
  <div id="app">
    <Bar />
    <Card name='Netflix'/>
    <Card name='Prime Video'/>
    <Card name='PLEX'/>
    <Card name='iPlayer'/>
    <Card name='Disney+'/>
    <Card name='Apple TV+'/>
  </div>
</template>

<script>
import Card from './components/Card.vue'
import Bar from './components/Bar.vue'

export default {
  name: "App",
  components: {
    Card,
    Bar
  }
};
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

  display: flex;
  flex-direction: column;
}
</style>
