// html
<template>
    <div class="card">
        <h1>{{name}}</h1>
    </div>
</template>

//js
<script>
export default {
  name: 'Tile',
  props: {
    name: String
  }
}
</script>

//css
<style scoped>

h1{
    /* color: red; */
    /* border: 2px solid violet; */
    display: inline;
}

.card{
  border: 2px solid black; 
  display: inline-block;
  padding: 20px;
  border-radius: 5px;
  background-color: violet;
}

</style>