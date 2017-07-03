<template>
  <div>{{message}}</div>
  <input v-model="message">
  <test-template></test-template>
</template>

<script>
  var inputTest = new Vue({
    el: '#input-test',
    data: {
      message: '안녕하세요 Vue!'
    }
  })
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
