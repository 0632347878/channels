<template>
  <div class="hello">
    <h1>This is homepage</h1>
    <h2>{{msg}}</h2>
    <button @click="goLogin" class="btn">login</button>
    <button @click="goRegister" class="btn">registration</button>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        msg: 'Hello World!'
      }
    },
    methods: {
      goLogin() {
        this.$router.push('login');
      },
      goRegister() {
        this.$router.push('register');
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  h1, h2 {
    font-weight: normal;
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
  .btn {
    padding: 5px 10px;
    background: transparent;
    border: 1px solid #666666;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
  }
</style>
