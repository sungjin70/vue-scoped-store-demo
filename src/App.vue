<template>
  <div id="app">
    <p>globalObject:{{globalObject}}</p>
    <p>globalCounter:{{globalCounter}}</p>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/page1">Page1</router-link> |
      <router-link to="/page2">Page2</router-link> |
      <router-link to="/page3">Page3</router-link> |
      <router-link to="/page4">Page4</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'App',
  data:function() {
    return {
      globalObject:{},
      globalCounter:-100,
    }
  },
  globalStore:{
    globalObject:{},
    globalCounter:{},
  }
});
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
  color: #42b983;
}
</style>
