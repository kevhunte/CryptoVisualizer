<template>
<div id="app">
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <Form msg="Encryption Visualizer" :output="this.temp" :iv="this.iv" :salt="this.salt" @cipher="initCipher" />

  <!--<div v-if="temp !== '' ">
    <strong>Output</strong><br>
    <strong id="iv">{{this.iv}}</strong><strong id="salt">{{this.salt}}</strong><strong id="output">{{this.temp}}</strong>
  </div>-->
  <!--Make Footer-->
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
      temp: '',
      iv: '',
      salt: ''
    }
  },
  mounted: function() {},
  methods: {
    initCipher(value) {
      const data = value;
      console.log(value);
      console.log(CryptoJS);
      if (value.encryption) { // encrypt
        this.Encrypt(data);
      } else { // decrypt
        this.Decrypt(data);
      }
    },
    Encrypt(body) {
      const key = body.key;
      const payload = body.payload;
      const keysize = body.keysize;
      const name = body.name;
      const blocksize = body.blocksize;
      const saltsize = body.saltsize;
      const ivsize = body.ivsize;
      const padding = body.paddings;
      //make iv / salt
      //choose algorithm
      const output = CryptoJS.AES.encrypt(payload, key).toString();

      //const output = CryptoJS.TripleDES.encrypt(payload, key).toString();

      //const output = CryptoJS.Rabbit.encrypt(payload, key).toString();

      this.temp = output;
      this.iv;
      this.salt;
      //console.log('AES No Params', this.temp);
    },
    Decrypt(body) {
      const key = body.key;
      const payload = body.payload;
      const keysize = body.keysize;
      const name = body.name;
      const blocksize = body.blocksize;
      const saltsize = body.saltsize;
      const ivsize = body.ivsize;
      const padding = body.paddings;
      //parse iv / salt
      //choose algorithm
      const output = CryptoJS.AES.decrypt(payload, key).toString();

      //const output = CryptoJS.TripleDES.decrypt(payload, key).toString();

      //const output = CryptoJS.Rabbit.decrypt(payload, key).toString();

      this.temp = output;
      this.iv;
      this.salt;
      //console.log('AES No Params', this.temp);
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
#output {
    /*purple*/
    color: #d63aff;
}
#iv {
    /*blue color*/
    color: #00b9f1;
}
#salt {
    /*red color*/
    color: #fb015b;
}
</style>
