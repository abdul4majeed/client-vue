<template>
  <div id="header">
    <div
      class="header-btn-holder d-flex justify-content-end align-items-center"
    >
      <nuxt-link to="/login">Login</nuxt-link>
      <nuxt-link to="/signup">Signup</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
#header {
  height: 50px;
  background-color: papayawhip;
  padding: 0rem 2rem;
}
.header-btn-holder {
  height: 50px;
}

#header a {
  text-decoration: none;
  padding: 0rem 0.3rem;
  color: black;
}

#header a:hover {
  color: blueviolet;
}
</style>
