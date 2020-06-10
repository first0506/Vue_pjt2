<template>
  <div class="container">
      <h1>회원가입</h1>
      <form @submit.prevent="signup" class="form-group">
          <p class="text-left"><label for="id">아이디</label></p>
          <input class="col form-control" id='id' type="text" aria-describedby="idHelp" v-model="signupData.username">
          <small id="idHelp" class="form-text text-muted">아이디를 작성해주세요.</small>
          <p class="text-left"><label for="pw1">비밀번호</label></p>
          <input class="col form-control" id="pw1" type="password" aria-describedby="pw1Help" v-model="signupData.password1">
          <small id="pw1Help" class="form-text text-muted">비밀번호를 작성해주세요.</small>
          <p class="text-left"><label for="pw2">비밀번호 확인</label></p>
          <input class="col form-control" id="pw2" type="password" aria-describedby="pw2Help" v-model="signupData.password2">
          <small id="pw2Help" class="form-text text-muted">비밀번호를 다시 한번 입력해주세요.</small><br>
          <button type="submit" class="btn btn-primary">확인</button>
      </form>
  </div>
</template>

<script>
export default {
    name: 'SignupView',
    data() {
        return {
            signupData: {
                username: null,
                password1: null,
                password2: null,
            }
        }
    },
    methods: {
        signup() {
            this.$emit('submit-signup-data', this.signupData)
        },
    },
}
</script>

<style>

</style>