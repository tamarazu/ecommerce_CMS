<template>
<div class="container-fluid">
  <div class="row d-flex justify-content-center" style="margin-top: 37px;margin-bottom: 11px;">
    <h1 class=" display-2 title-app">Jolie</h1>
  </div>
  <div class="row">
    <div class="col d-flex justify-content-center">
      <img src="../assets/undraw_mobile_login_ikmv.png" alt="" style="height: auto; width:auto">
    </div>
    <div class="col">
        <div class="modal-dialog text-center position-login">
          <div class="col-sm-20 main-section">
              <div class="modal-content">
                  <div class="col-12 form-input">
                      <form @submit.prevent="login">
                          <h1 class="login-text">LOGIN</h1>
                          <div class="form-group">
                              <input type="email" class="form-control" id="exampleInputEmail1" placeholder="Email" aria-describedby="emailHelp" v-model="email">
                              <small class="form-text text-muted">*We'll never share your email with anyone else.</small>
                          </div>
                          <div class="form-group">
                              <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="password">
                          </div>
                          <button type="submit" class="btn btn-success">Submit</button>
                      </form>
                  </div>
              </div>
            </div>
          </div>
    </div>

  </div>
</div>
</template>

<script>
import axiosCMS from '../config/index'

export default {
  name: 'LoginPanel',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login () {
      axiosCMS({
        method: 'post',
        url: '/login',
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(({ data }) => {
          localStorage.setItem('access_token', data.access_token)
          this.$router.push({ path: '/' })
        })
        .catch(({ response }) => {
          const data = response.data
          console.log(response)
          const error = data.error
          this.$vToastify.error(error)
        })
    }
  }
}
</script>

<style>

</style>
