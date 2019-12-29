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

  <div class="Enc-Engines">
    <strong>Select a Cipher to Get Started:</strong>
    <br>
    <b-dropdown v-b-popover.hover.top="'Symmetric Algorithms'" id="dropdown-1" :text="dropdownText" class="m-md-2">
      <b-dropdown-item :active="engine === 'AES'" v-b-toggle.AES-1 @click="setEngine('AES')">AES</b-dropdown-item>
      <b-dropdown-item :active="engine === 'Rijndael'" v-b-toggle.Rij-1 @click="setEngine('Rijndael')">Rijndael</b-dropdown-item>
      <b-dropdown-item :active="engine === 'Blowfish'" v-b-toggle.Blow-1 @click="setEngine('Blowfish')">Blowfish</b-dropdown-item>
      <b-dropdown-item :active="engine === 'RC4'" v-b-toggle.RC4-1 @click="setEngine('RC4')">RC4</b-dropdown-item>
    </b-dropdown>
    <!--Link multiple Id's on v-b-toggle for sequential collapses-->
    <b-collapse id="AES-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on AES Algorithm</p>
      <p class="card-text">AES contents Here: IV, Salt Size, Padding, Key Size</p>
    </b-collapse>
    <b-collapse id="Rij-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on Rijndael Algorithm</p>
      <p class="card-text">Rij contents Here: Block, IV, Salt Size, Padding, Key Size</p>
    </b-collapse>
    <b-collapse id="Blow-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on Blowfish Algorithm</p>
      <p class="card-text">Blow contents Here: IV, Salt Size, Padding, Key Size</p>
    </b-collapse>
    <b-collapse id="RC4-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on RC4 Algorithm</p>
      <p class="card-text">RC4 contents Here: IV, Salt Size, Padding, Key Size</p>
    </b-collapse>
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
      cipherMode: '',
      dropdownText: 'Cipher Engines'
    }
  },
  methods: {
    setEngine(val) {
      this.engine = val;
      this.dropdownText = val;
    }
  }
}
</script>
