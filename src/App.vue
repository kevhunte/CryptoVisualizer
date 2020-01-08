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
  mounted: function() {
    this.myEncrypt();
  },
  methods: {
    initCipher(value) {
      console.log(value);
      this.cipherData = value;
      //this.temp = val;
      /* Logic to implement cryptojs instances */
    },
    myEncrypt() {
      const key = 'password';
      const phrase = 'bananas';
      //var output = CryptoJS.AES.encrypt("bananas", "password").toString();
      console.log('SHA1 - ', CryptoJS.SHA1(phrase).toString());
      console.log(CryptoJS);
      console.log(CryptoJS.AES.encrypt(phrase, key));
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
