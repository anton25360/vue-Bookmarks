<template>
  <div id="app">
    <button class="FAicon fas fa-ellipsis-v" id="menuBtn"></button>
    <div id="menuContainer">
      <div id="menuNewTile" class="menuItem">
        <button class="FAicon fas fa-plus"></button> New tile
      </div>
      <div id="menuDeleteTile" class="menuItem">
        <button class="FAicon far fa-trash-alt" /> Delete tile
      </div>
      <div id="menuSettings" class="menuItem">
        <button class="FAicon fas fa-wrench" /> Settings
      </div>
    </div>

    <div id="introText">
      To get started, use the
      <div class="fas fa-ellipsis-v" />
      at the top of the screen.
    </div>

    <div id="tileGrid">
      <a
        v-bind:href="item[1]"
        target="_blank"
        class="tileContainer"
        v-for="item in tiles"
        v-bind:key="item"
        v-bind:style="{
          'background-image':
            'linear-gradient(145deg,' + item[2] + ',' + item[3] + ')',
        }"
      >
        <p id="boxLetter">{{ item[0].charAt(0) }}</p>
        <p id="boxName">{{ item[0] }}</p>
      </a>
    </div>

    <div id="modalBackground">
      <div id="modalContent">
        <div id="inputForm">
          <p class="inputTitle">NAME</p>
          <input type="text" id="inputName" placeholder="Name" /><br />
          <input type="text" id="inputLink" placeholder="URL" /><br />
          <p class="inputTitle">COLOURS</p>
          <p style="text-align: center">
            you can use words or hex codes.<br />Click
            <a id="uigLink" href="https://uigradients.com/">here</a> for
            inspiration.
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
          <p class="inputTitle">TILE</p>
          <div id="boxColourOutput">
            <p id="boxInitial"></p>
          </div>
        </div>

        <button id="modalCancelBtn">cancel</button>
        <button id="modalDoneBtn">Done</button>
      </div>
    </div>

    <div id="deleteModalBackground">
      <div id="deleteModalContent">
        <p class="inputTitle">DELETE</p>

        <div id="deleteTilesSelectionContainer">
          <select name="tilesSelection" id="deleteTilesSelection">
            <option v-for="item in tiles" v-bind:key="item">{{
              item[0]
            }}</option>
          </select>
        </div>

        <button id="deleteModalCancelBtn">cancel</button>
        <button id="deleteModalDoneBtn">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
//js here
window.onload = () => {
  setOutputBoxColour(); //set default colours of modal test output

  //create empty array if it doesnt already exist
  if (localStorage.getItem("tiles") == null) {
    localStorage.setItem("tiles", JSON.stringify([]));
  }

  //if array is empty, diplay welcome message + hide delete button
  if (JSON.parse(localStorage.getItem("tiles")).length == 0) {
    document.getElementById("introText").style.visibility = "visible";
    document.getElementById("menuDeleteTile").style.display = "none";
  }

let menuIsVisible = true

  //trigger colour chamge on key press:
  document.getElementById("inputColour1").onkeyup = setOutputBoxColour;
  document.getElementById("inputColour2").onkeyup = setOutputBoxColour;

  document.getElementById("inputName").onkeyup = setInitialLetter; //trigger initial(letter) onPress

  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal by default
  document.getElementById("deleteModalBackground").style.visibility = "hidden"; //hide delete modal by default

  document.getElementById("menuDeleteTile").onclick = () =>
    (document.getElementById("deleteModalBackground").style.visibility =
      "visible"); //open Delete Tile modal
  document.getElementById("menuNewTile").onclick = () =>
    (document.getElementById("modalBackground").style.visibility = "visible",
    document.getElementById("menuContainer").style.visibility = "hidden"); //open New Tile modal
  document.getElementById("modalCancelBtn").onclick = () =>
    (document.getElementById("modalBackground").style.visibility = "hidden"); //close New Tile modal
  document.getElementById("deleteModalCancelBtn").onclick = () =>
    (document.getElementById("deleteModalBackground").style.visibility =
      "hidden"); //close Delete Tile modal
  document.getElementById("menuBtn").onclick =()=> toggleMenuVisibility(menuIsVisible) //open Menu modal

  document.getElementById("modalDoneBtn").onclick = AddBookmark; //add bookmark to DB
  document.getElementById("deleteModalDoneBtn").onclick = DeleteBookmark; //add bookmark to DB

function toggleMenuVisibility(boolean) {
  if (boolean) {
    document.getElementById("menuContainer").style.visibility = "visible"
  } else {
        document.getElementById("menuContainer").style.visibility = "hidden"
  }
  menuIsVisible = !menuIsVisible
}


};

function AddBookmark() {
  let name = document.getElementById("inputName").value;
  let link = document.getElementById("inputLink").value;
  let colour1 = document.getElementById("inputColour1").value;
  let colour2 = document.getElementById("inputColour2").value;
  const nameCapitalized = name.charAt(0).toUpperCase() + name.slice(1);

  //check for HTTP or HTTPS
  if (link.includes("http://") || link.includes("https://")) {
    // do nothing
  } else {
    link = "https://" + link; //add https to the link's start
  }

  let dataArray = [nameCapitalized, link, colour1, colour2];

  let tilesArrayDecoded = JSON.parse(localStorage.getItem("tiles"));
  tilesArrayDecoded.push(dataArray);
  localStorage.setItem("tiles", JSON.stringify(tilesArrayDecoded));

  //clears input fields
  document.getElementById("inputName").value = "";
  document.getElementById("inputLink").value = "";

  location.reload();
}

function DeleteBookmark() {
  //gets selected value of drop down
  var element = document.getElementById("deleteTilesSelection");
  var chosenBookmark = element.options[element.selectedIndex].text;

  let tilesArrayDecoded = JSON.parse(localStorage.getItem("tiles")); //gets the tiles array from storage

  tilesArrayDecoded.forEach((element) => {
    //if chosen value from drop down exists
    if (element.includes(chosenBookmark)) {
      const index = tilesArrayDecoded.indexOf(element); //get index of element
      tilesArrayDecoded.splice(index, 1); //remove tile from array using index
      console.log("removed " + chosenBookmark);
    }
  });

  localStorage.setItem("tiles", JSON.stringify(tilesArrayDecoded)); //reset local tiles array
  location.reload();
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
  data() {
    return {
      tiles: JSON.parse(localStorage.getItem("tiles")),
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
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;

  background: linear-gradient(-45deg, #d3cce3, #e5ebff, #bcd4e7, #e2e2e2);
  background-size: 400% 400%;
  animation: gradient 5s ease infinite;
}
@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

#modalBackground,
#deleteModalBackground {
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */

  /* border: 2px solid blue; */
  display: flex;
  justify-content: center;
  align-items: center;
}
#modalContent,
#deleteModalContent {
  background-color: white;
  border-radius: 4px;
  display: inline-block;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#modalCancelBtn,
#deleteModalCancelBtn {
  float: left;
  font-family: "product";
  font-size: 17px;
  color: rgb(0, 81, 255);
  background-color: transparent;
  border: none;
  border-radius: 3px;
  padding: 5px 10px;
  margin: 10px;
}
#deleteModalCancelBtn {
  color: rgb(32, 32, 32);
}
#modalDoneBtn,
#deleteModalDoneBtn {
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

#deleteModalDoneBtn {
  background-color: rgb(238, 64, 98);
}

#modalDoneBtn,
#deleteModalCancelBtn,
#deleteModalDoneBtn,
#modalCancelBtn:hover {
  cursor: pointer;
}

#deleteTilesSelectionContainer {
  text-align: center;
}

#deleteTilesSelection {
  margin: 20px;
  font-size: 18px;
}

option {
  font-family: "product";
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
  margin: 20px;
}

#boxColourOutput {
  border-radius: 3px;
  margin: 0 auto;
  height: 150px;
  width: 150px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

  display: flex;
  justify-content: center;
  align-items: center;
}
/* in modal */
#boxInitial {
  font-size: 100px;
  color: rgba(255, 255, 255, 0.8);
  text-transform: uppercase;
}
#boxLetter {
  font-size: 100px;
  color: rgba(255, 255, 255, 0.8);
  text-transform: uppercase;
  /* border: 2px solid red; */
}

#boxName {
  position: absolute;
  margin-top: 195px;
  color: black;
}

#uigLink {
  text-decoration: none;
  color: rgb(0, 81, 255);
}

#tileGrid {
  /* border: 2px solid red; */
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 0 100px;
}

.tileContainer {
  margin: 30px;
  border-radius: 3px;
  height: 140px;
  width: 140px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;

  /* border: 3px solid red; */
  transition: all 0.2s ease-in-out;
}

.tileContainer:hover {
  transform: scale(1.05);
  /* cursor: pointer; */
}

#btnContainer {
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 20px;
}

.FAicon {
  background-color: transparent;
  border: none;
  outline: none;
}

#introText {
  position: absolute;
  visibility: hidden;
  font-size: 20px;
}

#introText div {
  font-size: 16px;
}
#menuBtn {
  font-size: 22px;
  position: absolute;
  top: 0px;
  right: 0px;
  margin: 10px;
  outline: none;
    cursor: pointer;

}
#menuContainer {
  position: absolute;
  top: 40px;
  right: 0px;
  margin-right: 10px;
  background-color: white;
  border-radius: 3px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  visibility: hidden;
  
}
.menuItem {
  cursor: pointer;
  padding: 10px;
}
.menuItem:hover {
  background-color: rgb(233, 233, 233);
}
</style>
