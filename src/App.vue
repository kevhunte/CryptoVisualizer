<template>
<div id="app">
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <Form msg="Encryption Visualizer" :output="this.temp" :iv="this.iv" :salt="this.salt" @cipher="initCipher" />

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
      }
    },
    Encrypt(body) {
      const key = body.key;
      const payload = body.payload;
      const keysize = body.keysize;
      const name = body.name;
      const ivsize = body.ivsize;
      const padding = body.paddings;
      const cm = body.ciphermode;
      let _iv = CryptoJS.lib.WordArray.random(ivsize);
      let mode;
      let pad;
      if (padding == 'PKCS7') {
        pad = CryptoJS.pad.Pkcs7;
      } else if (padding == 'ANSIX923') {
        pad = CryptoJS.pad.AnsiX923;
      } else if (padding == 'Zeroes') {
        pad = CryptoJS.pad.ZeroPadding;
      } else {
        pad = CryptoJS.pad.NoPadding;
      }

      if (cm == 'CFB') {
        mode = CryptoJS.mode.CFB;
      } else if (cm == 'OFB') {
        mode = CryptoJS.mode.OFB;
      } else if (cm == 'ECB') {
        mode = CryptoJS.mode.ECB;
      } else if (cm == 'CTR') {
        mode = CryptoJS.mode.CTR;
      } else {
        mode = CryptoJS.mode.CBC;
      }
      //set mode
      var output;
      if (name === 'AES') {
        output = CryptoJS.AES.encrypt(payload, key, {
          iv: _iv,
          padding: pad,
          mode: mode
        });
      } else if (name === '3DES') {
        output = CryptoJS.TripleDES.encrypt(payload, key, {
          iv: _iv,
          padding: pad,
          mode: mode
        });
      } else {
        output = CryptoJS.Rabbit.encrypt(payload, key, {
          iv: _iv,
          padding: pad,
          mode: mode
        });
      }

      /*console.log("text", output.ciphertext.toString());
      console.log("iv", output.iv.toString());
      console.log("salt", output.salt.toString());*/

      this.temp = output.ciphertext.toString();
      this.iv = output.iv.toString();
      this.salt = output.salt.toString();
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
