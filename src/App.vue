<template>
  <div id="nav" style="position:absolute; top:-25px; left:-20px;">
    <router-link to="/">Home</router-link> |
     <i class="bi bi-search"></i>
    <router-link to="/tasks">Tasks</router-link> |
   
  </div>
  <router-view/>
   
</template>
<script>
import Darkmode from 'darkmode-js';
new Darkmode().showWidget();


export default {
 
    
 
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
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #f29102;
}
</style>