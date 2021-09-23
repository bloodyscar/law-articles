<template>
<div v-on:scroll="scrollNavbar" class="navbr d-flex" id="navbar">
  <nav class="navbar navbar-expand-lg container d-flex justify-content-between align-items-center" >
      <img src="../assets//images/logo.png" width="70px">
      <ul class="navbar-nav d-none d-md-flex" id="navbar">
        <li class="nav-item active">
          <router-link class="nav-link" to="/">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="/articles">Articles</router-link>
        </li>
        
        <li class="nav-item">
          <a class="nav-link" href="#">Contact</a>
        </li>
      </ul>
  </nav>
</div>
</template>

<script>
export default {
    name: 'Navbar',
    props: ['CreateArticle'],
    created () {
      window.addEventListener('scroll', this.handleScroll);

    },
    methods: {
      handleScroll(){
        const nav = document.getElementById("navbar");
        nav.classList.toggle('sticky', window.scrollY > 0);
      },
    }
}

</script>

<style scoped>
  ul li a {
    color: #fff;
  }
</style>