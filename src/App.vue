<template>
  <div id="app">
    <p id="introText">To get started, use the + at the bottom of the screen.</p>
    <div id="btnContainer">
      <button class="FAicon far fa-trash-alt" id="newBookmarkBtn"></button>
      <button class="FAicon fas fa-plus" id="newBookmarkBtn"></button>
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
  </div>
</template>

<script>
// var testArray = ["one", "two", "three"];
console.log("script loaded");

//js here
window.onload = () => {
  setOutputBoxColour(); //set default colours of modal test output

  //create empty array if it doesnt already exist
  if (localStorage.getItem("tiles") == null) {
    localStorage.setItem("tiles", JSON.stringify([]));
  }

  //if array is empty, diplay welcome message
  if (JSON.parse(localStorage.getItem("tiles")).length == 0) {
    console.log("empty boi");
    document.getElementById("introText").style.visibility = "visible";
  } else {
    console.log("not empty");
  }

  //trigger colour chamge on key press:
  document.getElementById("inputColour1").onkeyup = setOutputBoxColour;
  document.getElementById("inputColour2").onkeyup = setOutputBoxColour;

  //trigger initial(letter) onPress
  document.getElementById("inputName").onkeyup = setInitialLetter;

  document.getElementById("modalBackground").style.visibility = "hidden"; //hide modal by default

  document.getElementById("newBookmarkBtn").onclick = openModal; //run createNewBookmark (opens modal)
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

  closeModal();
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
  justify-content: center;
  align-items: center;
  height: 100vh;
  /* background-color: aqua; */

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

  /* border: 2px solid blue; */
  display: flex;
  justify-content: center;
  align-items: center;
}
#modalContent {
  background-color: white;
  border-radius: 4px;
  display: inline-block;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#modalCancelBtn {
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
  font-size: 30px;
  background-color: transparent;
  border: none;

  color: #1b1d1f;
}

.FAicon {
  transition: all 0.2s ease-in-out;
}
.FAicon:hover {
  transform: scale(1.3);
  cursor: pointer;
}
#introText {
  position: absolute;
  visibility: hidden;
  font-size: 20px;
}
</style>
