<template>
  <div id="app">
    <div class="navBar">
      <p id="navTitle">Bookmarks</p>
      <p id="navBtn">New Bookmark</p>
    </div>

    <Tile name="test" link="x.com" colour1="red" colour2="blue" />

    <div id="tileGrid">
      <div class="tileContainer" v-for="item in tiles" v-bind:key="item">
        {{ item[0] }}
      </div>
    </div>

    <div id="modalBackground">
      <div id="modalContent">
        <div id="inputForm">
          <p class="inputTitle">TITLE</p>
          <input type="text" id="inputName" placeholder="Name" /><br />
          <input type="text" id="inputLink" placeholder="Web Adress" /><br />
          <p class="inputTitle">COLOURS</p>
          <p style="text-align: center">
            you can use words or hex codes.<br />Click
            <a href="https://uigradients.com/">here</a> for inspiration.
          </p>
          <input
            value="red"
            type="text"
            id="inputColour1"
            placeholder="eg: red"
          /><br />
          <input
            value="blue"
            type="text"
            id="inputColour2"
            placeholder="eg: blue"
          />
          <p class="inputTitle">OUTPUT</p>
          <div id="boxColourOutput">
            <p id="boxInitial"></p>
          </div>
        </div>

        <button id="modalCancelBtn">cancel</button>
        <button id="modalDoneBtn">Done</button>
      </div>
    </div>
  </div>
</template>

<script>
import Tile from "./components/Tile.vue";

// var testArray = ["one", "two", "three"];
console.log("script loaded");

//js here
window.onload = () => {
  setOutputBoxColour(); //set default colours

  //trigger colour chamge on key press:
  document.getElementById("inputColour1").onkeyup = setOutputBoxColour;
  document.getElementById("inputColour2").onkeyup = setOutputBoxColour;

  //trigger initial(letter) onPress
  document.getElementById("inputName").onkeyup = setInitialLetter;

  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal by default

  document.getElementById("navBtn").onclick = openModal; //run createNewBookmark (opens modal)
  document.getElementById("modalCancelBtn").onclick = closeModal; //add bookmark to DB and run closeModal (closes modal)
  document.getElementById("modalDoneBtn").onclick = AddBookmark; //add bookmark to DB and run closeModal (closes modal)
};

function openModal() {
  console.log("creating new bookmark...");
  document.getElementById("modalBackground").style.visibility = "visible";
}

function closeModal() {
  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal on close
}

function AddBookmark() {
  let name = document.getElementById("inputName").value;
  let link = document.getElementById("inputLink").value;
  let colour1 = document.getElementById("inputColour1").value;
  let colour2 = document.getElementById("inputColour2").value;

  let dataArray = [name, link, colour1, colour2];

  //create empty array if it doesnt already exist
  if (localStorage.getItem("tiles") == null) {
    localStorage.setItem("tiles", JSON.stringify([]));
  }

  let tilesArrayDecoded = JSON.parse(localStorage.getItem("tiles"));
  tilesArrayDecoded.push(dataArray);
  localStorage.setItem("tiles", JSON.stringify(tilesArrayDecoded));

  //clears input fields
  document.getElementById("inputName").value = "";
  document.getElementById("inputLink").value = "";

  closeModal();
}
function setOutputBoxColour() {
  let colour1 = document.getElementById("inputColour1").value;
  let colour2 = document.getElementById("inputColour2").value;

  document.getElementById("boxColourOutput").style.backgroundImage =
    "linear-gradient(145deg, " + colour1 + "," + colour2 + ")"; //sets colout of output box in modal
}

function setInitialLetter() {
  let initial = document.getElementById("inputName").value.charAt(0);
  console.log(initial);

  document.getElementById("boxInitial").innerText = initial;
}

export default {
  name: "App",
  components: {
    Tile,
  },
  data() {
    return {
      items: ["hello", "vue", "js"],
      fruits: ["apple", "pear", "bannana"],
      tiles: JSON.parse(localStorage.getItem("tiles")),
      // shoppingItems: [
      //   {name: 'apple', price: '10'},
      //   {name: 'orange', price: '12'}
      // ]
    };
  },
};
</script>

<style>
@font-face {
  font-family: "product";
  font-style: normal;
  font-weight: 400;
  src: local("Open Sans"), local("OpenSans"),
    url(https://fonts.gstatic.com/s/productsans/v5/HYvgU2fE2nRJvZ5JFAumwegdm0LZdjqr5-oayXSOefg.woff2)
      format("woff2");
}

#app {
  font-family: "product";
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
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */

  border: 2px solid blue;
  display: flex;
  justify-content: center;
  align-items: center;
}
#modalContent {
  /* visibility: hidden; */
  /* border: 2px solid red; */
  background-color: white;
  border-radius: 4px;
  display: inline-block;
  /* padding: 20px; */
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#modalCancelBtn {
  float: left;
  font-family: "product";
  /* font-weight: bold; */
  font-size: 17px;
  color: rgb(0, 81, 255);
  background-color: transparent;
  border: none;
  border-radius: 3px;
  padding: 5px 10px;
  margin: 10px;
}
#modalDoneBtn {
  float: right;
  font-family: "product";
  /* font-weight: bold; */
  font-size: 17px;
  color: white;
  background-color: rgb(0, 81, 255);
  border: none;
  border-radius: 3px;
  padding: 5px 10px;
  margin: 10px;
}

#modalDoneBtn,
#modalCancelBtn:hover {
  cursor: pointer;
}

input {
  font-family: "product";
  font-size: 18px;
  margin-bottom: 5px;
}

.inputTitle {
  text-align: center;
}

#inputForm {
  /* border: 2px solid blueviolet; */
  margin: 20px;
}

#boxColourOutput {
  /* border: 1px solid black; */
  border-radius: 3px;
  /* text-align: center; */
  margin: 0 auto;
  height: 150px;
  width: 150px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

  display: flex;
  justify-content: center;
  align-items: center;
}
#boxInitial {
  /* border: 2px solid red; */

  /* font-family: 'product'; */
  font-size: 100px;
  color: white;
  /* font-weight: bold; */
  text-transform: uppercase;
}
a {
  /* font-weight: 00; */
  text-decoration: none;
  color: rgb(0, 81, 255);
}

#tileGrid{
  border: 2px solid red;
}
.tileContainer{
  border: 2px solid blue;

}
</style>
