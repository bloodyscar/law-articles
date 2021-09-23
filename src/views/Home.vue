<template>
<div>
  <div class="hero">
    <Navbar/>
    <div class="container position-relative content">
        <vue-typed-js :strings="['^300 Law without Justice is <br> a Wound without Cure ^1000', 'The More Laws, <br> The Less Justice^1000']">
          <h1 class="typing text"></h1>
        </vue-typed-js>
        <vue-typed-js :strings="['^300 - William S. Downey^3300', '- Marcus T. Cicero']">
          <p class="typing text-white"></p>
        </vue-typed-js>
        <p class="text-white"></p>
        <router-link class="btn btn-primary btn-lg" to="/articles">Reads Article</router-link>
    </div>
  </div>
  <LatestUpdate/>
  <Highlight/>
  <Footer/>
</div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import LatestUpdate from '@/components/LatestUpdate.vue'
import Highlight from '@/components/Highlight.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'Home',
  components: {
    Navbar,
    LatestUpdate,
    Highlight,
    Footer
  },
}
</script>

