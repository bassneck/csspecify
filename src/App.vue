<template>
  <div id="app">
    <img src="./assets/logo.png" class="logo">
    <selector-form></selector-form>
  </div>
</template>

<script>
import SelectorForm from './components/SelectorForm';

export default {
  name: 'app',
  components: {
    SelectorForm,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

.logo {
  height: 120px;
}
</style>
