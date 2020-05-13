<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <loader/>
  </div>
</template>

<script>
  import Loader from "./components/Loader";
  export default {
  name: 'App',
  components: {Loader}
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
.btn--search {
  border: 1px solid rgba(102, 102, 102, 0.2);
  min-height: 43px;
  margin: 0;
}

 table,
 thead,
 tbody,
 tfoot,
 tr,
 th,
 td {
  height: auto;
  margin: 0;
  padding: 0;
  border: none;
  border-collapse: inherit;
  border-spacing: 0;
  border-color: inherit;
  vertical-align: inherit;
  text-align: left;
  font-weight: inherit;
  -webkit-border-horizontal-spacing: 0;
  -webkit-border-vertical-spacing: 0;
}
table {
  border-collapse: collapse;
}

table, th, td {
  border: 1px solid black;
}
</style>
