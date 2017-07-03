<!--vue init webpack [project name] 으로 프로젝트를 생성하면 webpack, hot reload, linting, testing, css extraction 을 생성-->
<!--이유는 알 수 없지만 index.html에서 직접적으로 Script Tag를 사용하지 않았다. npm run dev-->

<template>
  <div> <!--최상단의 Root Element를 두지 않으면 Error가 발생한다 -->
    <h1>{{msg}}</h1>
    <input v-model="msg">
    <button type="button" v-on:click="clickHandler">Test Event Listener</button> <!--Event Listenr 사용 법은 v-on:click 또는 @click (축약형) 과 같은 형태로 사용 가능-->
    <span v-bind:title="msg">Test Attribute Binding</span><br> <!--바인딩 사용법은 v-bind 또는 : (축약형) 으로 사용 가능-->
    <span :title="msg">Test Attribute Binding</span>
    <!--Template은 Vue.component로 정의할 수 있다. -->
    <ul>
      <test-template></test-template>
      <test-template></test-template>
      <test-template></test-template>
      <test-template></test-template>
      <!--props속성으로 template의 바인딩을 지정하 수 있다. -->
      <test-template-2 :msgmsg="msg"></test-template-2>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'test',
  data () {
    return {
      msg: 'Test Binding'
    }
  },

  methods: {
    clickHandler: function () {
      alert('clicked !')
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
