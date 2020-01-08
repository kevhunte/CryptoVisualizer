<template>
<div id="app">
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <Form msg="Encryption Visualizer" @cipher="initCipher" />
  {{cipherData}}
  {{temp}}
  <!--Instantiate engine and send to visualization component here-->
</div>
</template>

<script>
/*eslint-disable*/
import Form from './components/Form.vue';
import CryptoJS from "crypto-js";

export default {
  name: 'app',
  components: {
    Form
  },
  data() {
    return {
      cipherData: null,
      temp: '',
      CryptoJS
    }
  },
  methods: {
    initCipher(value) {
      console.log(value);
      this.cipherData = value;
      /*let output = this.CryptoJS.AES.encrypt("bananas", "password").toString();
      console.log(output);*/
      //this.temp = val;
      /* Logic to implement cryptojs instances */
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
