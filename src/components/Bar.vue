<template>
    <div class="appBar">
        <h1>Watchon</h1>
        <button id="infoButton">info</button>
    </div>
</template>

<script>
export default {
  name: 'Bar'
}

function logThis() {
    console.log('hello console');
}

document.getElementById('infoButton').onclick = logThis();
</script>

//css
<style scoped>

.appBar{
  border: 2px solid blue; 
  background-color: black;
}

h1{
    border: 2px solid black;
    display: inline;
    color: white;
}

button{
    border: 2px solid black;
    float: right;
}

</style>