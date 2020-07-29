<template>
  <div id="login">
    <h1>Login</h1>
    <p>(User: admin - Password: test)</p>
    <input
      type="text"
      name="username"
      v-model="input.username"
      placeholder="Username"
      :class="{ errorclass: errorlogin }"
    />
    <input
      type="password"
      name="password"
      v-model="input.password"
      placeholder="Password"
      :class="{ errorclass: errorpass }"
    />
    <button type="button" v-on:click="login()">Login</button>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      input: {
        username: '',
        password: '',
      },
      errorpass: false,
      errorlogin: false,
    };
  },

  methods: {
    login() {
      if (this.input.username !== '' && this.input.password !== '') {
        this.errorpass = false;
        this.errorlogin = false;
        if (
          this.input.username === this.$parent.mockAccount.username &&
          this.input.password === this.$parent.mockAccount.password
        ) {
          this.$emit('authenticated', true);
          this.$router.replace({ name: 'secure' });
        } else {
          alert('The username and / or password is incorrect');
        }
      } else {
        if (this.input.username === '' && this.input.password !== '') {
          this.errorpass = false;
          this.errorlogin = true;
        } else {
          if (this.input.username !== '' && this.input.password === '') {
            this.errorpass = true;
            this.errorlogin = false;
          }
        }
      }
    },
  },
};
</script>

<style scoped>
#login {
  display: flex;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande',
    'Lucida Sans Unicode', Geneva, Verdana, sans-serif;

  flex-direction: column;
  width: 500px;
  border: 1px solid #cccccc;
  background-color: #ffffff;
  margin: auto;
  margin-top: 200px;
  padding: 20px;
}
p {
  color: gray;
}
input {
  font-size: 1rem;
  margin: 10px 0;
  border-top: none;
  border-right: none;
  border-left: none;
  border-bottom: 1px solid #cccccc;

  padding: 1rem;
}
button {
  font-size: 1rem;
  margin: 10px 0;
  padding: 1rem;
  border: none;
  border: none;
}
button:hover {
  background-color: rgb(0, 95, 96);
  color: white;
}

.errorclass {
  border-bottom: 1px solid red;
}
</style>
