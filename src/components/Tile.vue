// html
<template>
  <div class="card">
    <h1>{{ name }} + {{ link }} + {{ colour1 }} + {{ colour2 }}</h1>
  </div>
</template>

//js
<script>
export default {
  name: "Tile",
  props: {
    name: String,
    link: String,
    colour1: String,
    colour2: String,
  },
};
</script>

<style scoped>
h1 {
  /* color: red; */
  /* border: 2px solid violet; */
  display: inline;
}

.card {
  border: 2px solid black;
  display: inline-block;
  padding: 20px;
  border-radius: 5px;
  background-color: violet;
}
</style>
