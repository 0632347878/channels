<template>
  <div v-if="loading" class="loader">
    <div class="lds-ripple">
      <div></div>
      <div></div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "loader",
    data() {
      return {
        loading: false
      }
    },

    mounted() {
      this.$root.$on('loader', (res) => this.loading = res)
    }
  }
</script>

<style scoped>
  .lds-ripple {
    display: inline-block;
    position: fixed;
    width: 80px;
    height: 80px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
  .loader {
    content: '';
    background: rgba(102, 102, 102, 0.6);
    position: fixed;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  .lds-ripple div {
    position: absolute;
    border: 4px solid #fff;
    opacity: 1;
    border-radius: 50%;
    animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
  }
  .lds-ripple div:nth-child(2) {
    animation-delay: -0.5s;
  }
  @keyframes lds-ripple {
    0% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 1;
    }
    100% {
      top: 0;
      left: 0;
      width: 72px;
      height: 72px;
      opacity: 0;
    }
  }
</style>
