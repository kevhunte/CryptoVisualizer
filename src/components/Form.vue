<style scoped lang="scss">
#form {
    padding: 0 15px;
}

h1 {
    margin: 0 0 40px;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>

<template>
<div id="form">
  <h1>{{ msg }}</h1>

  <div v-if="output !== '' ">
    <strong>Output</strong><br>
    <strong id="iv">{{iv}}</strong><strong id="salt">{{salt}}</strong><strong id="output">{{output}}</strong>
  </div>
  <br>

  <div class="Enc-Engines">
    <b-form-radio-group label="Input/Output" v-model="form.encryption" :options="[{text:'Encryption',value:true},{text:'Decryption',value:false}]" plain name="enc-radios">
    </b-form-radio-group>
    <div id="alg-groups">
      <div id="aes-group" class="w-responsive text-center mx-auto p-3 mt-2">
        <b-button-group>
          <b-button @click="setData('AES',128)" variant="primary">AES-128</b-button>
          <b-button @click="setData('AES',192)" variant="primary">AES-192</b-button>
          <b-button @click="setData('AES',256)" variant="primary">AES-256</b-button>
        </b-button-group>
      </div>

      <div id="3des-group" class="w-responsive text-center mx-auto p-3 mt-2">
        <b-button-group>
          <b-button @click="setData('3DES',56)" variant="info">3DES-56</b-button>
          <b-button @click="setData('3DES',112)" variant="info">3DES-112</b-button>
          <b-button @click="setData('3DES',168)" variant="info">3DES-168</b-button>
        </b-button-group>
      </div>

      <div id="rabbit-group" class="w-responsive text-center mx-auto p-3 mt-2">
        <b-button-group>
          <b-button @click="setData('Rabbit',128)" variant="outline-primary">Rabbit</b-button>
        </b-button-group>
      </div>
    </div>
    <div id="algorithm-options" class="w-responsive text-center mx-auto p-3 mt-2">
      <b-button-group>
        <b-dropdown right text="IV Size">
          <b-dropdown-item :active="form.ivsize === i" @click="setVal('iv', i)" v-for="i in sizes" :key="i">{{i}} Bits</b-dropdown-item>
        </b-dropdown>
      </b-button-group>
      <b-button-group>
        <b-dropdown right text="Salt Size">
          <b-dropdown-item :active="form.saltsize === s" @click="setVal('salt', s)" v-for="s in sizes" :key="s">{{s}} Bits</b-dropdown-item>
        </b-dropdown>
      </b-button-group>
      <br><br>
      <b-button-group>
        <b-dropdown right text="Cipher Mode">
          <b-dropdown-item :active="form.ciphermode === m" @click="setVal('ciph', m)" v-for="m in modes" :key="m">{{m}}</b-dropdown-item>
        </b-dropdown>
      </b-button-group>
      <b-button-group>
        <b-dropdown right text="Block Size">
          <b-dropdown-item :active="form.blocksize === b" @click="setVal('block', b)" v-for="b in blocksizes" :key="b">{{b}} Bits</b-dropdown-item>
        </b-dropdown>
      </b-button-group>
      <b-button-group>
        <b-dropdown right text="Paddings">
          <b-dropdown-item :active="form.paddings === p" @click="setVal('pad', p)" v-for="p in paddingtypes" :key="p">{{p}}</b-dropdown-item>
        </b-dropdown>
      </b-button-group>
    </div>

    <b-form-group class="w-responsive text-center mx-auto p-3 mt-2" id="input-text-group">
      <b-form-input v-model="form.key" placeholder="Enter key here"></b-form-input>
      <b-form-input v-model="form.payload" placeholder="Enter payload"></b-form-input>
      <br>
      <b-button @click="onSubmit" variant="outline-success">Execute</b-button>
      <b-button @click="onReset" variant="outline-danger">Reset</b-button>
    </b-form-group>
  </div>
</div>
</template>

<script>
/*eslint-disable*/

export default {
  name: 'Form',
  props: {
    msg: String,
    output: String,
    iv: String,
    salt: String
  },
  components: {},
  data() {
    return {
      dropdownText: 'Cipher Engines',
      sizes: [16, 32, 64],
      keysizes: [128, 192, 256],
      blocksizes: [64, 128, 256],
      paddingtypes: ['Zeroes', 'PKCS7', 'ANSIX923'],
      modes: ['ECB', 'CBC', 'CTR', 'CFB', 'OFB'],
      form: {
        encryption: true,
        name: '',
        keysize: null,
        blocksize: null,
        saltsize: null,
        ciphermode: null,
        ivsize: null,
        paddings: null,
        payload: '',
        key: ''
      },
    }
  },
  methods: {
    setData(name, keysize) {
      this.form.name = name;
      this.form.keysize = keysize;
    },
    setVal(name, val) {
      let f = this.form;
      if (name === 'block') {
        f.blocksize = val;
      } else if (name === 'iv') {
        f.ivsize = val;
      } else if (name === 'salt') {
        f.saltsize = val;
      } else if (name === 'ciph') {
        f.ciphermode = val;
      } else if (name === 'pad') {
        f.paddings = val;
      } else if (name === 'payload') {
        f.payload = val;
      } else if (name === 'key') {
        f.key = val;
      }
    },
    onReset(evt) {
      evt.preventDefault();
      this.form.encryption = true;
      this.form.name = '';
      this.form.keysize = null;
      this.form.blocksize = null;
      this.form.saltsize = null;
      this.form.ivsize = null;
      this.form.ciphermode = null;
      this.form.paddings = null;
      this.form.payload = '';
      this.form.key = '';
    },
    onSubmit(evt) {
      evt.preventDefault();
      //pass up to App.vue
      let copy = {
        ...this.form
      };
      this.$emit('cipher', copy); // passes unique copy to parent
    }
  }
}
</script>
