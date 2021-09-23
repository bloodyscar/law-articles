<template>
  <div>
    <div style=" background-color: #424242;">
        <Navbar />
    </div>
    <div class="container" style="margin-top:100px;">
      <div class="row">
        <div class="col-md-8">
          <h3 class="mb-3">Create New article</h3>
          <div class="card">
            <div class="card-body">
              <form action="" @submit.prevent="setBlogs">
                <div class="form-group">
                  <label for="title">Title</label>
                  <input type="text" v-model="blogs.title" id="title" class="form-control">
                </div>
                <div class="form-group">
                  <label for="body">Body</label>
                  <textarea type="text" v-model="blogs.body" id="body" class="form-control"></textarea>
                </div>
                <div class="form-group">
                  <label for="thumbnail">Thumbnail</label>
                  <input type="file" @change="onFileSelected" id="thumbnail" class="form-control-file">
                </div>
                <div class="form-group">
                  <label for="tag">Tags</label>
                  <select class="form-control" v-model="blogs.tags" multiple >
                    <option disabled selected>--- Pilih Tags ---</option>
                    <option v-for="option in options" :key="option.id" :value="option.id">{{option.name}}</option>
                  </select>
                </div>
                <button type="submit" class="btn btn-primary mt-3">Create</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios'
export default {
    name: 'CreateArticle',
    components:{
      Navbar,
      Footer,
    },
    data(){
      return{
        blogs:{
          title: null,
          body: null,
          tags: [],
        },
        thumbnail: null,
        options: [
          {id: 1, name:'Pidana'},
          {id: 2, name:'Perdata'},
          {id: 3, name:'Legal'},
          {id: 4, name:'Public'},
        ]
      }
    },
    methods:{
      setBlogs(){
        const fd = new FormData();
        fd.append('title', this.blogs.title);
        fd.append('body', this.blogs.body);
        fd.append('thumbnail', this.thumbnail);
        for (let i = 0; i < this.blogs.tags.length; i++) {
          fd.append('tags[]', this.blogs.tags[i]);
          
        }
        const token = localStorage.getItem('token')
        axios.post('http://127.0.0.1:8000/api/article/create', fd ,{
          headers: {
            'Authorization': 'Bearer ' + token}
        })
        .then((response) => {
          console.log(response);
        })

      },
      onFileSelected(data){
        this.thumbnail = data.target.files[0]
      },
    },
}
</script>

<style>

</style>

