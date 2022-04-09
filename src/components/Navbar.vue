<template>
  <nav class="main-nav">
      <router-link :to="{name: 'Home'}">Projects</router-link>
      <router-link :to="{name: 'AddProject'}">Add New Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
.main-nav {
  background: #fff;
  padding: 0 20px;
  border-bottom: 1px solid #ddd;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
}

.main-nav a {
  color: #555;
  text-decoration: none;
  display: inline-block;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  letter-spacing: 1px;
  transition: all 0.3s ease-in-out;
}

a.router-link-active {
  background: #eee;
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>