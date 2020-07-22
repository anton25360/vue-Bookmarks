// html
<template>
    <div class="card">
        <h1>test one: {{test1}}</h1>
        <h1>test two: {{test2}}</h1>
    </div>
</template>

//js
<script>
export default {
  name: 'Card',
  props: {
    test1: String,
    test2: String
  }
}
</script>

//css
<style scoped>

h1{
    color: aqua;
}
</style>