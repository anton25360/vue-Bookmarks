<template>
  <div id="app">
    <div class="navBar">
      <p>Bookmarks2</p>
      <button id="newBookmarkBtn">HELLO</button>
    </div>

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

export default {
  name: "App",
  components: {
    Card
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
  padding: 0;
  margin: 0;

  display: flex;
  flex-direction: column;
}

.navBar{
  border: 2px solid blue;

}
</style>
