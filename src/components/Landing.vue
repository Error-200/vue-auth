<template>


 <div class="jumbotron text-center">
  <div class="container">
        <h1>HELLO {{ name }}</h1>
        <h2> successfully logged in </h2>
      <h3>using email: {{ email }}</h3>

    <hr>

    <button @click="logout">logout</button>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'Landing',
  data() {
    return {
      name: '',
      email: '',
    }
  },
  created() {
    //user is not authorized
    if (localStorage.getItem('token') === null) {
      this.$router.push('/login');
    }
  },
  mounted() {
    axios.get('http://localhost:5000/user', { headers: { token: localStorage.getItem('token')}})
      .then(res => {
        this.name = res.data.user.name;
        this.email = res.data.user.email;
      })
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push('/login');
    }
  }
}
</script>
