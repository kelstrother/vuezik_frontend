<template>
  <div class="home">
    <p class="listener">{{ name }}</p>
      <h1>Vuezaak</h1>
      <router-link to='/about'>About</router-link>
      <div class="console">
      </div>
      <br>
      <button class='btn-logout' @click="Logout">Logout</button>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import firebase from 'firebase'

export default {
  setup () {
    const user = firebase.auth().currentUser

    const name = ref('');

    onBeforeMount(() => {
      const user = firebase.auth().currentUser;
      if (user) {
        name.value = user.email.split('@')[0]
      }
    })
    const Logout = () => {
      firebase
      .auth()
      .signOut()
      .then(() => console.log("Signed Out"))
      .catch(err => alert(err.message))
    }
    return {
      name,
      Logout
    }
  }
}

</script>

<style lang="scss" scoped>
p {
  text-align: left;
}
.home {
  background: rgb(28,72,111);
  background: linear-gradient(180deg, rgba(28,72,111,1) 0%, rgba(5,55,111,1) 21%, rgba(30,34,40,1) 87%); 
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  background-color: #2c3e50;
  height: 100vh;
  color: #f4f4f4;

    a { 
      color: #f4f4f4;
    }
    .btn-logout { 
      padding: .5em;
      margin-top: 4em;
      border: none;
  }
}
</style>
