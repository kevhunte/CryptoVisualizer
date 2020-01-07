<template>
<div id="app">
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <Form msg="Encryption Visualizer" @cipher="initCipher" />
  {{cipherData}}
  <!--Instantiate engine and send to visualization component here-->
</div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  /*eslint-disable*/
  name: 'app',
  components: {
    Form
  },
  data() {
    return {
      cipherData: null
    }
  },
  methods: {
    initCipher(value) {
      console.log(value);
      this.cipherData = value;
    }
  }
}
</script>

<style lang="scss">
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
