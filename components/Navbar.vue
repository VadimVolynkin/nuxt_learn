<template>
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Nuxt SSR</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item">
        <nuxt-link exact no-prefetch active-class="active" class="nav-link" to="/">
            Home
        </nuxt-link>
      </li>
      <li class="nav-item">
        <nuxt-link active-class="active" class="nav-link" to="/about">
            About
        </nuxt-link>
      </li>
      <li class="nav-item">
        <nuxt-link active-class="active" class="nav-link" to="/users">
            Users
        </nuxt-link>
      </li>
      <li class="nav-item" v-if="!hasToken">
        <nuxt-link active-class="active" class="nav-link" to="/login">
            Login
        </nuxt-link>
      </li>
      <li active-class="active" class="nav-link" v-else>
        <a @click.prevent="logout" href="#">Logout</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
</template>

<script>
export default {
  computed: {
    hasToken() {
      return this.$store.getters.hasToken
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('logout')
      this.$router.push('/login')
    }
  }
}
</script>

<style>

</style>


// TODO не работает no-prefetch in nuxt-link