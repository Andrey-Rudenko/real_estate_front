<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700&display=swap" rel="stylesheet">
  <header-log-page></header-log-page>

  <div class="container container-1 d-flex justify-content-center rounded">
    <form class="frm" action="" @submit.prevent="authorize">
      <div class="row justify-content-center ">
        <p class="p-header ">Вход</p>
      </div>

      <div class="row name-input">
        <p class="p-name ">Логин</p>
      </div>

      <div class="row">
        <input
            class="form-control inp "
            type="text"
            placeholder="Введите логин"
            v-model="login"
        >
      </div>

      <div class="row name-input">
        <p class="p-name ">Пароль</p>
      </div>
      <div class="row">
        <input
            class="form-control inp"
            type="password"
            placeholder="Введите пароль"
            v-model="password"
        >
      </div>

      <div class="btn-div row justify-content-center">
        <button class="btn btn-primary">Войти</button>
      </div>

    </form>
  </div>

  <div class="container container-2 d-flex justify-content-center rounded">
    <div class="link-div row justify-content-center ">
      <p class="p-link">Еще нет аккаунта? <router-link to="/reg"> Зарегистрироваться </router-link></p>
    </div>  </div>
</template>


<script>

import axios from "axios";

export default {
  name: "LoginPage",
  data() {
    return {
      isAuthorized: localStorage.getItem('token') != null,
      login: '',
      password: '',
      token: '',
    }
  },
  methods: {
    authorize() {
      axios.post('http://95.154.68.102/api/token/login/',{
        username: this.login,
        password: this.password
      }).then((response) => {
        localStorage.setItem('token', response.data.auth_token);
        axios.defaults.headers.common['Authorization'] = `Token ${response.data.auth_token}`
        this.$router.push('/')
      }).catch(function () {
        alert("Неправильный логин/пароль")
      })
    },
  }
}
</script>


<style scoped>
.container-1{
  margin-top: 60px;
  box-shadow: -1px -1px 5px rgb(191, 191, 191), 1px 1px 5px rgb(191, 191, 191);
  max-width: 500px;
}

.container-2{
  margin-top: 25px;
  box-shadow: -1px -1px 5px rgb(191, 191, 191), 1px 1px 5px rgb(191, 191, 191);
  max-width: 500px;
}

.btn-div{
  margin-top: 60px;
  margin-bottom: 50px;
}

.btn{
  width: 300px;
  height: 54px;
  color: black;
  background-color:white;
  border-width: 2px;
  border-color: #5F77BF;
}

.btn:hover{
  width: 300px;
  height: 54px;
  color: white;
  background-color: #5F77BF;
  border-color: #5F77BF;
}

.btn:active {
  width: 300px;
  height: 54px;
  color: black;
  background-color:white;
  border-width: 2px;
  border-color: #5F77BF;
}

.btn:focus {
  box-shadow: none !important;
}


.p-header{
  width: auto;
  margin: auto;
  font-family: 'Inter',serif;
  font-style: normal;
  font-weight: 400;
  font-size: 52px;
  line-height: 75px;
}

.link-div{
  margin-top: 20px;
  margin-bottom: 20px;
}

.link{
  width: auto;
  cursor: pointer;
  font-family: 'Inter',serif;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 22px;
  color: #5F77BF;
  text-decoration: none;
}

.link:hover{
  text-decoration: underline;

}

.p-link{
  margin: auto;
  width: auto;
  font-family: 'Inter',serif;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 22px;
  text-decoration: none;
}

.p-name{
  font-family: 'Inter',serif;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 30px;
  margin-bottom: auto;
  padding: 0;
}

.name-input{
  margin-top: 50px;
}

.inp{
  width: 380px;
  height: 50px;
  border-color: #5F77BF;
}

@media screen and (max-width: 550px) {
  body { zoom: 100%; }
}

</style>