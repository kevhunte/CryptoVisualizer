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
      //console.log(CryptoJS);
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
      let _iv = CryptoJS.lib.WordArray.random(ivsize);
      let _salt = CryptoJS.lib.WordArray.random(saltsize);;
      //make iv / salt
      //set mode and padding
      var output;
      if (name === 'AES') {
        output = CryptoJS.AES.encrypt(payload, key, {
          iv: _iv,
          salt: _salt
        });
      } else if (name === '3DES') {
        output = CryptoJS.TripleDES.encrypt(payload, key, {
          iv: _iv,
          salt: _salt
        });
      } else {
        output = CryptoJS.Rabbit.encrypt(payload, key, {
          iv: _iv,
          salt: _salt
        });
      }

      /*console.log("text", output.ciphertext.toString());
      console.log("iv", output.iv.toString());
      console.log("salt", output.salt.toString());*/

      this.temp = output.ciphertext.toString();
      this.iv = output.iv.toString();
      this.salt = output.salt.toString();
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
      let _iv;
      let _salt;
      //parse iv / salt
      //set mode and padding
      let output; // payload needs to come as object with iv and salt
      if (name === 'AES') {
        output = CryptoJS.AES.decrypt(payload, key);
      } else if (name === '3DES') {
        output = CryptoJS.TripleDES.decrypt(payload, key);
      } else {
        output = CryptoJS.Rabbit.decrypt(payload, key);
      }

      console.log(output);

      if (output) {
        this.temp = output.toString(CryptoJS.enc.Utf8);
        //this.iv = output.iv.toString();
        //this.salt = output.salt.toString();
        //console.log('AES No Params', this.temp);
      }

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
