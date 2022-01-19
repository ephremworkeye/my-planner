<template>
<nav class="main-nav">
  <router-link :to="{ name: 'Home' }">Projects</router-link>
  <router-link :to="{ name: 'AddProject' }">Add Project</router-link>
</nav>
</template>

<script>
export default {

}
</script>

<style>
    .main-nav {
        text-align: center;
        margin: 40px auto;
    }
    .main-nav a{
        display: inline-block;
        text-decoration: none;
        margin: 0 10px;
        color: rgb(57, 55, 55);
        font-size: 18px;
    }
    a.router-link-active {
        border-bottom: 2px solid green;
        padding-bottom: 4px;
        color: black;
    }
</style>