<template>
  <div id="secure">
    <form>
      <input type="text" v-model="company" placeholder="Introduce compañía" />
      <button v-on:click="getUsers">Search</button>
    </form>
    <div>
      <table className="table">
        <thead>
          <tr v-if="users !== null">
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
      users: null,
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
  width: 50px;
  border-radius: 1rem;
}
th {
  color: green;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande',
    'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
td {
  color: orange;
  width: 200px;
  text-align: center;
  padding: 20px;
}
button {
  background-color: green;
  border: none;
  color: white;
  font-size: 1rem;
  margin-left: 50px;
  padding: 1rem;
  width: 250px;
}
button:hover {
  background-color: grey;
  cursor: pointer;
  border: none;
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
</style>
