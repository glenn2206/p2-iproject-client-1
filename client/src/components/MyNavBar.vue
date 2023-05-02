<template>
<div class="position-relative">
  <nav class="position-fixed w-100 navbar navbar-expand-sm bg-dark navbar-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav">
        <li class="nav-item">
          <router-link class="nav-link active" to="/">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link active" to="/login">Login</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link active" to="/travelpost" v-if="role === 'admin'">PostTravel</router-link>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="" v-on:click.prevent='logoutClick'>Logout</a>
        </li>
        <li class="nav-item">
          <router-link class="nav-link active" to="/travelplace">TravelPlace</router-link>
        </li>
      </ul>
      </div>
    </div>
  </nav>
  <div style="height: 55px;"></div>
</div>
</template>

<script>
export default {
  name: 'NavBar',
  methods: {
    logoutClick () {
      localStorage.clear()
      this.$router.push({ path: '/login' })
    }
  },
  computed: {
    role () {
      return this.$store.state.role
    }
  }
}
</script>

<style>
.position-fixed {
  z-index: 999;
}
</style>
