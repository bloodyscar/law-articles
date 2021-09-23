<template>
  <div>
    <div style="background-color:#424242;">
      <Navbar />
    </div>
    <div class="container" style="margin-top: 50px;">
      <div class="row">
        <div class="col-md-9">
          <Breadcrumb/>
        </div>
        <div class="col-md-2">
          <a href="/articles/create" class="btn btn-primary">New Article</a>
        </div>
      </div>
      
      <h2 class="font-weight-bold">Our Article's</h2>

      <!-- Start Pagination  -->
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item" >
            <a class="page-link" href="#" aria-label="Previous" >
              <span aria-hidden="true" class="paginat3">&laquo;</span>
              <span class="sr-only">Previous</span>
            </a>
          </li>
          <li class="page-item"><a class="page-link paginat3" href="#">1</a></li>
          <li class="page-item"><a class="page-link paginat3" href="#">2</a></li>
          <li class="page-item"><a class="page-link paginat3" href="#">3</a></li>
          <li class="page-item" >
            <a class="page-link" href="#" aria-label="Next" >
              <span aria-hidden="true" class="paginat3">&raquo;</span>
              <span class="sr-only">Next</span>
            </a>
          </li>
        </ul>
      </nav>
      <!-- End Pagination  -->

      <div class="row">
          <div class="col-md-8">
              <div v-for="listArticle in listArticles" :key="listArticle.id">
                  <CardList :listArticle="listArticle"/>
              </div>
          </div>
          <div class="col-md-1">

          </div>
          <div class="col-md-3">
            <div>
              <Sidebar />
            </div>
          </div>

      </div>
    </div>
    <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Breadcrumb from "@/components/Breadcrumb.vue";
import CardList from "@/components/CardList.vue";
import axios from 'axios';
import Footer from '@/components/Footer.vue'
import Sidebar from '@/components/Sidebar.vue'

export default {
  name: "Articles",
  components: {
    Navbar,
    Breadcrumb,
    CardList,
    Sidebar,
    Footer,
  },
  data(){
    return{
      listArticles: [],
    }
  },
  methods : {
    setListArticles(data){
      this.listArticles = data;
    },
  },
  mounted(){
    axios.get('http://127.0.0.1:8000/api/articles' )
    .then((response) => {
      this.setListArticles(response.data.data)
    })
    .catch((error) => {
      console.log(error.message)
    })
  }
};
</script>

<style scoped>
  .paginat3{
    color: black;
  }

  ul li a.paginat3{
    color: black;
  }
</style>