<template>
    <section class="vh-100" style='background-color: #FFE53B;
background-image: linear-gradient(147deg, #FFE53B 0%, #FF2525 74%);
'>
  <div class="container-fluid h-custom">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col-md-9 col-lg-6 col-xl-5">
        <img src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.webp" class="img-fluid"
          alt="Sample image">
      </div>
      <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1">
        <form v-on:submit.prevent="registerSubmit">

          <!-- Email input -->
          <div class="form-outline mb-4">
            <input type="email" id="form3Example3" class="form-control form-control-lg"
              placeholder="Enter a valid email address" v-model="formRegister.email"/>
            <label class="form-label" for="form3Example3">Email address</label>
          </div>

          <!-- Password input -->
          <div class="form-outline mb-3">
            <input type="password" id="form3Example4" class="form-control form-control-lg"
              placeholder="Enter password" v-model="formRegister.password"/>
            <label class="form-label" for="form3Example4">Password</label>
          </div>

          <div class="text-center text-lg-start mt-4 pt-2">
            <button type="submit" class="btn btn-primary btn-lg"
              style="padding-left: 2.5rem; padding-right: 2.5rem;">Register</button>
            <p class="small fw-bold mt-2 pt-1 mb-0">Back to Login <a v-on:click.prevent='goLoginPage' href=""
                class="link">Login</a></p>
          </div>

        </form>
      </div>
    </div>
  </div>
</section>
</template>

<script>
export default {
  name: 'RegisterPage',
  data () {
    return {
      formRegister: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    goLoginPage () {
      this.$router.push({ path: '/login' })
    },
    registerSubmit () {
      this.$store.dispatch('registerSubmit', this.formRegister)
        .then(data => {
          this.formRegister.email = ''
          this.formRegister.password = ''
          this.$swal.fire({
            icon: 'success',
            title: 'Register Successfully',
            text: 'Welcome'
          })
          this.$router.push({ path: '/login' })
        })
        .catch(err => {
          this.$swal.fire({
            icon: 'error',
            title: 'Register Failed',
            text: `${err.response.data.message}`
          })
        })
    }
  }
}
</script>

<style>

</style>
