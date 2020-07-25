<template>
  <div id="nav">
      <router-link to="/">To Do</router-link> |
      <router-link to="/about">About</router-link>
</div> 
</template>
<script>
export default {
    name:"Header"
}
</script>
<style scoped>
  
#nav {
  padding: 30px;
  text-align: center;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>