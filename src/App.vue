<template>
  <div id="app">
    <div id="nav">
      <div class="text-left">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </div>

    </div>
    <router-view/>
  </div>
</template>

<script>
  export default {
    created() {
      if(localStorage.getItem('code')){
        this.$router.push('/result')
      }
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
  font-size: 0.8rem;
}

.text-left{
  text-align: left;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
