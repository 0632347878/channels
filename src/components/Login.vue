<template>
  <div>
    <h4>Login</h4>
    <form>
      <label for="email" >E-Mail Address</label>
      <div>
        <input id="email" type="email" v-model="email" required autofocus>
      </div>
      <div>
        <label for="password" >Password</label>
        <div>
          <input id="password" type="password" v-model="password" required>
        </div>
      </div>
      <div ref="auth">
        <button type="submit" @click="handleSubmit" class="btn">Login</button>
        <button v-if="unauthorized" @click="goRegister" class="btn btn--error">registration</button>
        <p v-if="unauthorized" class="error">You should apply registration</p>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        email : "",
        password : "",
        unauthorized: false
      }
    },
    methods : {
      handleSubmit(e){
        e.preventDefault();
        if (this.password.length > 0) {
          this.$http.post('http://localhost:3000/login', {
            email: this.email,
            password: this.password
          })
        .then(response => {
          let is_admin = response.data.user.is_admin;
          localStorage.setItem('user',JSON.stringify(response.data.user));
            localStorage.setItem('jwt',response.data.token);
            if (localStorage.getItem('jwt') != null) {
              this.$emit('loggedIn');
              if(this.$route.params.nextUrl != null){
                this.$router.push(this.$route.params.nextUrl)
              }
              else {
                this.$router.push('dashboard')
              }
            }
          })
          .catch((error) => {
            console.error(error.response);
            this.unauthorized = true;
          });
        }
      },
      goRegister() {
        this.$router.push('register');
      }
    }
  }
</script>

<style>
  .error {
    color: red;
  }
</style>
