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
    <div>
      <!--v-once를 사용하면 1회만 변경된다-->
      <span v-once>다시는 변경하지 않습니다: {{ msg }}</span>
      <!--HTML 을 입력하기 위해서는 v-html 디렉티브를 사용해야 한다-->
      <div v-html="rawHtml"></div>
      <!--바인딩에서는 Javascript 표현식을 사용할 수 있다-->
      <div>{{msg ? 'OK' : 'NO'}}</div>
      <!--v-if 디렉티브를 이용하여 DOM 엘리먼트를 제거 및 삽입 할 수 있다-->
      <div v-if="msg ? true : false">MSG를 지우면 사라짐</div>
      <!-- | 기호로 간단한 필터 기능을 사용할 수 있다. filters Property안에 method를 넣어야 한다-->
      <div>{{msg | msgConvert}}</div>
      <!-- 필터는 텍스트에 대한 간단한 변화를 하기 위해 만들어졌으며 복잡한 연산 또는 별도의 Property처럼 사용하기 위해서는 Computed를 사용-->
      <!-- computed property를 통해 사용한다. 종속성이 있는 Property가 있을 경우에만 재계산 되는 것이 특징이다.-->
      <div>{{computedMessage}}</div>
      <!--watch property를 이용해 특정 property의 변화를 감지할 수 있다-->
      <div>Watch : {{msgWatch}}</div>
      <!--클래스 Binding을 할 수 있다.-->
      <div :class="{active: isActive}">123</div>
      <!--꼭 인라인 형태가 아니더라도 상관이 없다-->
      <div :class="classObject">123</div>
      <!--템플릿과 같이 사용하는 경우 템플릿 정의할 때 추가된 class와 템플릿 사용시 정의한 class가 합쳐져 나온다-->
      <!--인라인 스타일 바인딩도 class와 동일한 방식으로 사용 가능하다-->
      <div></div>
      <!-- v-if v-else-if v-else디렉티브로 제어할 수 있다-->
      <div v-if="cnt%4 === 0">0</div>
      <div v-else-if="cnt%4 === 1">1</div>
      <div v-else-if="cnt%4 === 2">2</div>
      <div v-else>3</div>

      <!--Vue에서는 아래의 경우에서 다시 화면을 렌더링 하지 않고 데이터만을 바꿔준다 -->
      <template v-if="isActive">
        <label>사용자 이름</label>
        <input placeholder="사용자 이름을 입력하세요">
      </template>
      <template v-else>
        <label>이메일</label>
        <input placeholder="이메일 주소를 입력하세요">
      </template>

      <!--만약 재사용하지 않기를 원한다면 Key 속성을 넣어주면 된다. 이때 label은 재사용하게 된다. -->
      <template v-if="isActive">
        <label>사용자 이름</label>
        <input placeholder="사용자 이름을 입력하세요" key="username-input">
      </template>
      <template v-else>
        <label>이메일</label>
        <input placeholder="이메일 주소를 입력하세요" key="email-input">
      </template>

      <!-- v-if 와 v-show의 차이 -->
      <!-- v-if는 조건부 렌더딩, v-show는 렌더링 후 CSS 기반 토글 -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'test',
  data () {
    return {
      msg: 'Test Binding',
      rawHtml: '<h1>hi</h1>',
      msgWatch: '',
      isActive: true,
      cnt: 0
    }
  },

  methods: {
    clickHandler: function () {
      alert('clicked !')
    }
  },

  filters: {
    msgConvert: function (value) {
      return 'filter value ' + value
    }
  },

  computed: {
    computedMessage: function () {
      return 'computed message : ' + this.msg + new Date()
    },
    classObject: function () {
      return {
        active: this.isActive
      }
    }
  },

  watch: {
    msg: function (newMsg) {
      this.msgWatch = newMsg
      this.isActive = !this.isActive
      this.cnt++
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.active {
  color: blue;
}
</style>
