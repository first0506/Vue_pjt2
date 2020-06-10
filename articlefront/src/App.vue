<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'List' }">목록으로</router-link> |
      <span v-if="isLogin">
        <router-link to="/accounts/logout" @click.native="logout">Logout</router-link>
      </span>
      <span v-else>
        <router-link to="/accounts/login">Login</router-link> |
        <router-link to="/accounts/signup">Signup</router-link>
      </span>
    </div>
    <router-view
      @submit-login-data="login"
      @submit-signup-data="signup"
    />
  </div>
</template>

<script>
import axios from 'axios'

const SERVER_URL = "http://127.0.0.1:8000"

export default {
  name: 'App',
  data() {
    return {
      isLogin: false
    }
  },
  created() {
    if (this.$cookies.isKey('auth-token')) {
      this.isLogin = true
      this.$router.push('/articles')
    } else {
      this.isLogin = false
    }
  },
  methods: {
    setCookie(key) {
      this.$cookies.set('auth-token', key)
      this.isLogin = true
    },
    signup(signupData) {
      axios.post(`${SERVER_URL}/rest-auth/signup/`, signupData)
        .then(response => {
          this.setCookie(response.data.key)
          this.$router.push('/articles')
        })
        .catch(error => console.log(error.response))
    },
    login(loginData) {
      axios.post(`${SERVER_URL}/rest-auth/login/`, loginData)
        .then(response => {
          this.setCookie(response.data.key)
          this.$router.push('/articles')
        })
        .catch(error => console.log(error.response))
    },
    logout() {
      const requestHeader = {
        headers: {
          Authorization: `Token ${this.$cookies.get('auth-token')}`
        }
      }
      axios.post(`${SERVER_URL}/rest-auth/logout/`, null, requestHeader)
        .then(() => {
          this.$cookies.remove('auth-token')
          this.isLogin = false
          this.$router.push('/articles')

        })
        .catch(error => console.log(error.response))
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
