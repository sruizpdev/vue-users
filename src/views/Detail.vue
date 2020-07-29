<template>
  <div id="detail">
    <h2>Detail page</h2>
    <p>id: {{ user.id }}</p>
    <p>login: {{ user.login }}</p>
    <img class="imagen" :src="user.avatar_url" alt="" />
    <p>company: {user.company}</p>
    <router-link to="/secure">{{ user.login }}Back to list</router-link>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Detail',
  props: {
    login: String,
  },
  data: function() {
    return {
      user: {},
    };
  },
  mounted() {
    this.login = this.$route.params.login;

    axios
      .get(`https://api.github.com/users/${this.login}`)
      .then((response) => (this.user = response.data));
  },
};
</script>
