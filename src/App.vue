<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.btn {
  margin: 5px 0;
  padding: 5px 10px;
  background: transparent;
  border: 1px solid #666666;
  border-radius: 5px;
  cursor: pointer;
  outline: none;
}
.btn--error {
  color: red;
  border-color: red;
}
</style>
