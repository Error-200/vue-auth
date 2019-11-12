<template>
<div class="container mt-5">
  <h1>Register</h1>



  <div class="row">
    <div class="col-sm-8">
      <div class="card">
        <div class="card-body">


             <div class="form-group">
              <label for="name">Name</label>
              <input type="text" class="form-control"  v-model="name">
               </div>

            <div class="form-group">
              <label for="email">Email  </label>
              <input type="email" class="form-control"  v-model="email">
            </div>


            <div class="form-group">
              <label for="phone">PHONE NUMBER</label>
              <input type="" class="form-control"  v-model="phone" >
            </div>

            <div class="form-group">
              <label for="password">Password  </label>
              <input type="password" class="form-control" v-model="password">
            </div>





            <button @click="signup">signup</button>
            {{ error }}




        </div>
      </div>
    </div>
    </div>
  </div>

</template>


<script>
import axios from 'axios';

export default {
  name: 'Signup',
  data() {
    return {
      name: '',
      email: '',
      phone: '',
      password: '',


      error: '',
    }
  },
  methods: {

    signup() {
      let newUser = {
        name: this.name,
        email: this.email,
        phone: this.phone,
        password: this.password

      }
      axios.post('http://localhost:5000/signup', newUser)
        .then(res => {
          this.error = '';
          this.$router.push('/login');
        }, err => {
          console.log(err.response)
          this.error = err.response.data.error
        })
    }
  }
}
</script>

<style>
body {
  background-color: #E8ECEF;
}
.centered {
    padding-top: 200px;
    text-align: center;
}

.secret-text {
  text-align: center;
  font-size: 2rem;
  color: #fff;
  background-color: #000;
}
</style>
