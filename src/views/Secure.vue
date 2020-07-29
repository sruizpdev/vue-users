<template>
  <div id="secure">
    <form>
      <input type="text" v-model="company" />
      <button v-on:click="getUsers">Search</button>
    </form>
    <div>
      <table className="table">
        <thead>
          <tr>
            <th>Avatar</th>
            <th>Id</th>
            <th>Name</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>
              <img class="imagen" :src="user.avatar_url" alt="" />
            </td>
            <td>
              <span>{{ user.id }}</span>
            </td>
            <td>
              <button v-on:click="navigate(user.login)">
                {{ user.login }}
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Secure',

  data() {
    return {
      users: [],
      company: '',
      error: false,
      mock: [],
    };
  },
  methods: {
    navigate(login) {
      console.log(login);
      this.$router.push({
        name: 'detail',
        params: {
          login: login,
        },
      });
    },
    getUsers(e) {
      e.preventDefault();
      if (this.company !== '') {
        axios
          .get(`https://api.github.com/orgs/${this.company}/members`)
          .then((response) => (this.users = response.data));
      } else {
        alert('Debes rellenar el campo de busqueda');
      }
    },
  },
};
</script>

<style scoped>
#secure {
  background-color: #ffffff;
  border: 1px solid #cccccc;
  padding: 20px;
  margin-top: 10px;
}
.imagen {
  width: 100px;
  border-radius: 1rem;
}
</style>
