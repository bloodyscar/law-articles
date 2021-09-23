<template>
  <div>
    <div style=" background-color: #424242;">
        <Navbar />
    </div>
    <div class="container" style="margin-top:100px;">
      <div class="row">
        <div class="col-md-8">
          <h3 class="mb-3">Edit article</h3>
          <div class="card">
            <div class="card-body">
              <form method="POST" enctype="multipart/form-data" action="">
                <div class="form-group">
                  <label for="title">Title</label>
                  <input v-model="title" type="text" id="title" class="form-control">
                </div>
                <div class="form-group">
                  <label for="body">Body</label>
                  <textarea v-model="body" type="text" id="body" class="form-control"></textarea>
                </div>
                <div class="form-group">
                  <label for="thumbnail">Thumbnail</label>
                  <input type="file" @change="updateThumbnail" name="thumbnail" id="thumbnail" class="form-control-file">
                </div>
                <div class="form-group">
                  <label for="tag">Tags : <span  v-for="tag in tags" :key="tag.id"> #{{ tag.name }}</span> </label>
                  <select v-model="tags" class="form-control" multiple="multiple">
                    <!-- <option v-for="item in tags" :key="item.id" selected>
                      {{item.name}}
                    </option> -->
                    <option v-for="option in options" :key="option.id" v-bind:value="option.id">
                      {{option.name}}
                    </option>
                  </select>
                </div>
                <button type="submit" @click.prevent="updateBlogs" class="btn btn-primary mt-3">Update</button>
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
    name: 'EditArticle',
    components:{
        Navbar,
        Footer
    },
    data(){
        return{
            title: '',
            body: '',
            thumbnail: null,
            tags: [],
            
            options: [
              {id: 1, name:'Pidana'},
              {id: 2, name:'Perdata'},
              {id: 3, name:'Legal'},
              {id: 4, name:'Public'},
            ],
        }
    },
    methods:{
      tagSelected(){
        console.log(this.options)
      },
      setBlogs(data){
        this.title = data.title
        this.body = data.body
        let tag = this.tags
        for (let i = 0; i < data.tags.length; i++) {
          tag.push(data.tags[i])
        }
        // console.log(this.thumbnail)
      },
      updateBlogs() {
      let fd = new FormData()
      fd.append('title', this.title)
      fd.append('body', this.body)
      fd.append('thumbnail', this.thumbnail)
      for (let i = 0; i < this.tags.length; i++) {
          fd.append('tags[]', this.tags[i]);
          
        }
      fd.append('_method', 'PATCH')

      const token = localStorage.getItem('token')
      axios.post(`http://127.0.0.1:8000/api/article/update/${this.$route.params.slug}`, fd , {
          headers: {
            'Authorization': 'Bearer ' + token,
            }
        })
      .then(() => {
        this.$router.push('/articles')
      }).catch(error => console.log(error.message))
      },
      updateThumbnail(e){
        this.thumbnail = e.target.files[0];
        
      }
    },
    mounted(){
      axios.get('http://127.0.0.1:8000/api/show/' + this.$route.params.slug)
      .then(response => {
        this.setBlogs(response.data.data);
      }).catch(e => console.log(e.message));
    }
}
</script>

<style>

</style>