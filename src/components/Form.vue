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
    <b-form-radio-group label="Input/Output" v-model="form.encryption" :options="[{text:'Encryption',value:true},{text:'Decryption',value:false}]" plain name="enc-radios">
    </b-form-radio-group>
    <br>
    <strong>Select a Cipher:</strong>
    <br>

    <b-dropdown v-b-popover.hover.top="'Symmetric Algorithms'" id="dropdown-1" :text="dropdownText" class="m-md-2">
      <b-dropdown-item :active="engine === 'AES'" v-b-toggle.AES-1 @click="setEngine('AES')">AES</b-dropdown-item>
      <b-dropdown-item :active="engine === 'Rijndael'" v-b-toggle.Rij-1 @click="setEngine('Rijndael')">Rijndael</b-dropdown-item>
      <b-dropdown-item :active="engine === 'Twofish'" v-b-toggle.Two-1 @click="setEngine('Twofish')">Twofish</b-dropdown-item>
    </b-dropdown>
    <!--Link multiple Id's on v-b-toggle for sequential collapses-->
    <b-collapse id="AES-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on AES Algorithm</p>
      <!--<p class="card-text">AES contents Here: IV, Salt Size, Padding, Key Size</p>-->
      <div class="form-container">
        <b-form @submit="onSubmit" @reset="onReset">
          <b-form-group id="aes-group-1" label="Key Size*:" label-for="aes-1" description="All computations are done in the browser.">
            <b-form-select id="aes-1" v-model="form.keysize" :options="keysizes" required placeholder="Enter email"></b-form-select>
          </b-form-group>

          <!--<b-form-group id="rij-group-2" label="Block Size*:" label-for="rij-2" description="The size of the returned output.">
            <b-form-select id="rij-2" v-model="form.blocksize" :options="blocksizes" required placeholder="Enter name"></b-form-select>
          </b-form-group>-->

          <b-form-group id="aes-group-2" label="Salt Size:" label-for="aes-2" description="The amount of random bits appended to the ciphertext.">
            <b-form-select id="aes-2" v-model="form.saltsize" :options="sizes" placeholder="Enter name"></b-form-select>
          </b-form-group>

          <b-form-group id="aes-group-3" label="Cipher Mode*:" label-for="aes-3" description="The ciphermode used for the Algorithm.">
            <b-form-select id="aes-3" v-model="form.ciphermode" :options="modes" required></b-form-select>
          </b-form-group>

          <b-form-group id="aes-group-4" v-if="this.form.ciphermode !== 'none' && this.form.ciphermode !== null" label="IV Size:" label-for="aes-4" description="The amount of bits used as the first step of this encryption mode.">
            <b-form-select id="aes-4" v-model="form.ivsize" :options="sizes"></b-form-select>
          </b-form-group>

          <b-form-group id="aes-group-4" label="Padding Type:" label-for="aes-4" description="The spacing needed between blocks.">
            <b-form-select id="aes-4" v-model="form.paddings" :options="paddingtypes"></b-form-select>
          </b-form-group>

          <b-button type="submit" variant="success">Initialize Cipher</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
      </div>
    </b-collapse>

    <b-collapse id="Rij-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on Rijndael Algorithm</p>
      <div class="form-container">
        <b-form @submit="onSubmit" @reset="onReset">
          <b-form-group id="rij-group-1" label="Key Size*:" label-for="rij-1" description="All computations are done in the browser.">
            <b-form-select id="rij-1" v-model="form.keysize" :options="keysizes" required placeholder="Enter email"></b-form-select>
          </b-form-group>

          <b-form-group id="rij-group-2" label="Block Size*:" label-for="rij-2" description="The size of the returned output.">
            <b-form-select id="rij-2" v-model="form.blocksize" :options="blocksizes" required placeholder="Enter name"></b-form-select>
          </b-form-group>

          <b-form-group id="rij-group-3" label="Salt Size:" label-for="rij-3" description="The amount of random bits appended to the ciphertext.">
            <b-form-select id="rij-3" v-model="form.saltsize" :options="sizes" placeholder="Enter name"></b-form-select>
          </b-form-group>

          <b-form-group id="rij-group-4" label="Cipher Mode*:" label-for="rij-4" description="The ciphermode used for the Algorithm.">
            <b-form-select id="rij-4" v-model="form.ciphermode" :options="modes" required></b-form-select>
          </b-form-group>

          <b-form-group id="rij-group-5" v-if="this.form.ciphermode !== 'none' && this.form.ciphermode !== null" label="IV Size:" label-for="rij-5" description="The amount of bits used as the first step of this encryption mode.">
            <b-form-select id="rij-5" v-model="form.ivsize" :options="sizes"></b-form-select>
          </b-form-group>

          <b-form-group id="rij-group-6" label="Padding Type:" label-for="rij-6" description="The spacing needed between blocks.">
            <b-form-select id="rij-6" v-model="form.paddings" :options="paddingtypes"></b-form-select>
          </b-form-group>

          <b-button type="submit" variant="success">Initialize Cipher</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
      </div>
    </b-collapse>
    <b-collapse id="Two-1" accordion="alg-accordion" class="mt-2">
      <p class="card-text">Blurb on Twofish Algorithm</p>
      <p class="card-text">Twofish contents Here: IV, Salt Size, Padding, Key Size</p>
      <div class="form-container">
        <b-form @submit="onSubmit" @reset="onReset">
          <b-form-group id="two-group-1" label="Key Size*:" label-for="two-1" description="All computations are done in the browser.">
            <b-form-select id="two-1" v-model="form.keysize" :options="[128,256]" required placeholder="Enter email"></b-form-select>
          </b-form-group>

          <b-form-group id="two-group-2" label="Block Size*:" label-for="two-2" description="The size of the returned output.">
            <b-form-select id="two-2" v-model="form.blocksize" :options="[128]" required placeholder="Enter name"></b-form-select>
          </b-form-group>

          <b-form-group id="two-group-3" label="Salt Size:" label-for="two-3" description="The amount of random bits appended to the ciphertext.">
            <b-form-select id="two-3" v-model="form.saltsize" :options="sizes" placeholder="Enter name"></b-form-select>
          </b-form-group>

          <b-form-group id="two-group-4" label="Cipher Mode*:" label-for="two-4" description="The ciphermode used for the Algorithm.">
            <b-form-select id="two-4" v-model="form.ciphermode" :options="modes" required></b-form-select>
          </b-form-group>

          <b-form-group id="two-group-5" v-if="this.form.ciphermode !== 'none' && this.form.ciphermode !== null" label="IV Size:" label-for="two-5" description="The amount of bits used as the first step of this encryption mode.">
            <b-form-select id="two-5" v-model="form.ivsize" :options="sizes"></b-form-select>
          </b-form-group>

          <b-form-group id="two-group-6" label="Padding Type:" label-for="two-6" description="The spacing needed between blocks.">
            <b-form-select id="two-6" v-model="form.paddings" :options="paddingtypes"></b-form-select>
          </b-form-group>

          <b-button type="submit" variant="success">Initialize Cipher</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
      </div>
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
      dropdownText: 'Cipher Engines',
      sizes: [16, 32],
      keysizes: [128, 192, 256],
      blocksizes: [128, 256],
      paddingtypes: ['none', 'PKCS7', 'ANSIX923'],
      modes: ['ECB', 'CBC', 'CTR', 'CFB', 'OFB'],
      form: {
        encryption: true,
        name: '',
        keysize: null,
        blocksize: null,
        saltsize: null,
        ciphermode: null,
        ivsize: null,
        paddings: null
      },
    }
  },
  methods: {
    setEngine(val) {
      this.engine = val;
      this.dropdownText = val;
      this.form.name = val;
    },
    onReset(evt) {
      evt.preventDefault();
      this.form.encryption = true;
      this.form.keysize = null;
      this.form.blocksize = null;
      this.form.saltsize = null;
      this.form.ivsize = null;
      this.form.ciphermode = null;
      this.form.paddings = null;
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
