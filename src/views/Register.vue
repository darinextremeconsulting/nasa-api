<script setup>
  import { ref } from 'vue'
  import * as firebase from 'firebase/app'
  import { useRouter } from 'vue-router'

  console.log(firebase) // Undefined

  const email = ref('')
  const password = ref('')
  const router = useRouter()
  const register = () => {
    try {
      firebase
        .auth()
        .createUserWithEmailAndPassword(email.value, password.value)
        .then((data) => {
          console.log('Successfully registered!')
          router.push('/Home')
        })
        .catch((error) => {
          console.log(error.code)
          alert(error.message)
        })
    } catch (error) {
      console.log(error)
    }
  }
</script>
<template>
  <v-container class="grey lighten-5 mt-16 mb-6">
    <v-row>
      <v-col cols="12 text-center">
        <h1>Create an Account</h1>
        <p><input type="text" placeholder="Email" v-model="email" /></p>
        <p>
          <input type="password" placeholder="Password" v-model="password" />
        </p>
        <p><button class="button" @click="register">Submit</button></p>
      </v-col>
    </v-row>
  </v-container>
</template>
<style scoped>
  input[type='text'],
  input[type='password'] {
    width: 200px;
    height: 39px;
    -webkit-border-radius: 0px 4px 4px 0px/5px 5px 4px 4px;
    -moz-border-radius: 0px 4px 4px 0px/0px 0px 4px 4px;
    border-radius: 0px 4px 4px 0px/5px 5px 4px 4px;
    background-color: #fff;
    -webkit-box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.09);
    -moz-box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.09);
    box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.09);
    border: solid 1px #cbc9c9;
    margin-left: -5px;
    margin-top: 13px;
    padding-left: 10px;
  }

  input[type='password'] {
    margin-bottom: 25px;
  }

  .button {
    background-color: #4caf50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
  }
</style>
