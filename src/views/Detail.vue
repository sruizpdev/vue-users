<template>
  <div id="detail">
    <h2>Detail page</h2>
    <p>id: {{ user.id }}</p>
    <p>login: {{ user.login }}</p>
    <img class="imagen" :src="user.avatar_url" alt="" />

    <router-link to="/secure" class="volver">Back to search >>></router-link>
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
<style scoped>
#detail {
  border: 1px solid gray;
  padding: 10px 30px;
  background-color: white;
  width: 400px;
  margin-top: 50px;
}
h2,
p {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande',
    'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
p {
  font-weight: bold;
}
.imagen {
  width: 200px;
  display: block;
  margin-bottom: 50px;
}
.volver {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande',
    'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  text-decoration: none;
}
</style>
