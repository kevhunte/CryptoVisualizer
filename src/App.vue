<template>
<div id="app">
  <!--<img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <Form msg="Encryption Visualizer" />
  <!--Listener to grab form data and set cryptojs instance accordingly.
  Instantiate engine and send to visualization component-->
</div>
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'app',
  components: {
    Form
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
