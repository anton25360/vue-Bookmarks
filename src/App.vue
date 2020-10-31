<template>
  <div id="app">
    <div class="navBar">
      <p id="navTitle">Bookmarks</p>
      <p id="navBtn">New Bookmark</p>
    </div>

    <Card name="Netflix" />
    <Card name="Prime Video" />
    <Card name="PLEX" />
    <Card name="iPlayer" />
    <Card name="Disney+" />
    <Card name="Apple TV+" />

    <div id="modalBackground">
      <div id="modalContent">
        <p>hello i am modal</p>
        <button id="modalCloseBtn">close me</button>
      </div>
    </div>

  </div>
</template>

<script>
import Card from "./components/Card.vue";

console.log("script loaded");

//js here
window.onload = () => {
  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal by default

  document.getElementById("navBtn").onclick = createNewBookmark; //run createNewBookmark
  document.getElementById("modalCloseBtn").onclick = closeModal; //run closeModal
};

function createNewBookmark() {
  console.log("creating new bookmark...");
  document.getElementById("modalBackground").style.visibility = "visible";
}

function closeModal() {
  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal on close
}

export default {
  name: "App",
  components: {
    Card,
  },
};
</script>

<style>
@font-face {
  font-family: "Product Sans";
  font-style: normal;
  font-weight: 400;
  src: local("Open Sans"), local("OpenSans"),
    url(https://fonts.gstatic.com/s/productsans/v5/HYvgU2fE2nRJvZ5JFAumwegdm0LZdjqr5-oayXSOefg.woff2)
      format("woff2");
}

#app {
  font-family: "Product Sans";
  padding: 0;
  margin: 0;

  display: flex;
  flex-direction: column;
}

.navBar {
  background-color: #2c3e50;
}

#navTitle {
  color: white;
  float: left;
  font-size: 20px;
  margin-left: 20px;
}

#navBtn {
  float: right;
  background-color: white;
  color: #2c3e50;
  padding: 5px 10px;
  border-radius: 3px;
  margin-right: 20px;
}
#navBtn:hover {
  cursor: pointer;
}

#modalBackground {
  /* visibility: hidden; */
  /* display: none; */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */

  border: 2px solid red;
}
#modalContent {
  /* visibility: hidden; */
  border: 2px solid red;
  background-color: white;
}
</style>
