<template>
  <div class="container">
      <h1>로그인</h1>
      <form @submit.prevent="login" class="form-group">
          <p class="text-left"><label for="id">아이디</label></p>
          <input class="col form-control" id='id' type="text" v-model="loginData.username"><br>
          <p class="text-left"><label for="pw">비밀번호</label></p>
          <input class="col form-control" id="pw" type="password" v-model="loginData.password"><br>
          <div class="text-left"><button type="submit" class="btn btn-primary">확인</button></div>
        
      </form>
  </div>
</template>

<script>
export default {
    name: 'LoginView',
    data() {
        return {
            loginData: {
                username: null,
                password: null,
            }
        }
    },
    methods: {
        login() {
            this.$emit('submit-login-data', this.loginData)
        },
    },
}
</script>

<style>

</style>