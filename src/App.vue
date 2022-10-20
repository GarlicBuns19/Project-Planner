<template>
  <Navbar/>
  <router-view/>
</template>
<script>
import Navbar from './components/Navbar.vue'
export default{
  components : {
    Navbar
  }
}
</script>
<style>
body{
  background-image: url(https://i.postimg.cc/cJRQp6HK/hex.jpg);
  /* background-repeat: no-repeat; */
  background-position: center;
  background-size: cover;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  max-width: 600px;
  margin: 0 auto;
  color: #efefef;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  text-decoration: none;
  color: #efefef;
}

a.router-link-exact-active {
  border-bottom: 4px solid #42b983;
  padding: 0px 0 10px 0;
  /* color: #42b983; */
}
</style>
