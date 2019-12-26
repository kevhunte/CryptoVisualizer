<style scoped lang="scss">
.m-md-3 {}

#form {
    padding: 0 15px;
}

h3 {
    margin: 40px 0 0;
    font-size: 20px;
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
  <h3>Start By Selecting an Encryption Engine</h3>

  <div class="Enc-Engines">
    <strong>Select from the list here:</strong>

    <b-dropdown id="dropdown-1" text="Cipher Engines" class="m-md-2">
      <b-dropdown-item @click="setEngine('AES')">AES</b-dropdown-item>
      <b-dropdown-item @click="setEngine('Rij')">Rijndael</b-dropdown-item>
      <b-dropdown-item @click="setEngine('Blow')">Blowfish</b-dropdown-item>
    </b-dropdown>
    {{engine}}
  </div>
</div>
</template>

<script>
/*eslint-disable*/
export default {
  name: 'Form',
  props: {
    msg: String
  },
  data() {
    return {
      engine: '',
      cipherMode: ''
    }
  },
  methods: {
    setEngine(val) {
      this.engine = val;
    }
  }
}
</script>
