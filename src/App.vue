<template>
  <div id="app">
    <div class="navBar">
      <p id="navTitle">Bookmarks</p>
      <p id="navBtn">New Bookmark</p>
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

@font-face {
  font-family: 'Product Sans';
  font-style: normal;
  font-weight: 400;
  src: local('Open Sans'), local('OpenSans'), url(https://fonts.gstatic.com/s/productsans/v5/HYvgU2fE2nRJvZ5JFAumwegdm0LZdjqr5-oayXSOefg.woff2) format('woff2');
}

#app {


  font-family: 'Product Sans';
  /* text-align: center; */
  padding: 0;
  margin: 0;

  display: flex;
  flex-direction: column;
}

.navBar{
  /* border: 2px solid blue; */
  background-color: #2c3e50;
  /* padding: 10px; */


}

#navTitle{
  color: white;
  float: left;
  font-size: 20px;
  margin-left: 20px;
}

#navBtn{
  float: right;
  background-color: white;
  color: #2c3e50;
  padding: 5px 10px;
  border-radius: 3px;
  margin-right: 20px;



  
}
</style>
