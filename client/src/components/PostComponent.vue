<template>
  <div class="container">
    
      
      <h1 class="title" >Create a Post</h1>
      
    
    
      <div class="create-post">
        <textarea
          class="input-style"
          id="create-post"
          v-model="text"
          placeholder="Say something..."
          rows="4"
        ></textarea>
        <button class="btn" v-on:click="createPost">Post</button>
      </div>
    
    
  
    <p class="error" v-if="error">{{ error }}</p>
    
    <div class="post-list">
      <!--Div below represents each indivudal post-->
      <div class="post" v-for="(post, index) in posts" 
      v-bind:item="post" 
      v-bind:index="index"
      v-bind:key="post._id"
      v-on:dblclick="deletePost(post._id)"
      >
      <div class="post-header">{{ `${post.createdAt.getDate()}/${post.createdAt.getMonth()}/${post.createdAt.getFullYear()}` }}</div>
        
      <div class="post-content" style="word-wrap: break-word;"> {{ post.text }}</div>
      </div>
    </div>
    
    <v-snackbar v-model="showToastr" :timeout="this.timeout" color="green" location="bottom right">
        {{ toastrText }}
    </v-snackbar>
  </div>
  
</template>

<script>
// may need to dot dot slash
import PostService from '@/PostService';

export default {
  name: 'PostComponent',
  data(){
    return {
      posts: [],
      error: '',
      text: '',
      timeout: 3500,
      showToastr: false
    }
  },
  async created() {
    try {
      this.posts = await PostService.getPosts();
    } catch(err) {
      this.error = err.message;
    }
  },
  methods: {
    async createPost(){
      await PostService.insertPost(this.text);
      this.posts = await PostService.getPosts()
      this.text = ''
    },
    async deletePost(id){
      await PostService.deletePost(id);
      this.posts = await PostService.getPosts()
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
@import url('https://fonts.cdnfonts.com/css/bukhari-script');
.container {
  max-width: 800px;
  margin: 0 auto;
}

.title {
  font-size: 5rem;
  text-align: center;
  margin-bottom: 2rem;
  color: #a2d5ff;
  -webkit-text-stroke: 0.1px #ffffff;
  font-family: 'Bukhari Script', sans-serif;
  
}

.create-post {
  margin-bottom: 2rem;
}

.input-style {
  width: 95%;
  border: 5px solid #a86a24;
  border-radius: 10px;
  padding: 1rem;
  font-size: 1.5rem;
  font: bold;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  resize: none;
  color: #a86a24;
  font-family: 'Bukhari Script', sans-serif;
}

.btn {
  display: inline-block;
  background-color: #a86a24;
  color: #ffffff;
  font-size: 1rem;
  width: 200px;
  font-weight: 500;
  border: none;
  border-radius: 10px;
  padding: 0.75rem 1.5rem;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border: 3px solid #ffffff;
  
}

.btn:hover {
  background-color: #0d8bd0;
}


.btn-delete:hover {
  background-color: #d71c0c;
}

.post {
  border-radius: 10px;
  border: 3px solid #a2d5ff;
  padding: 1rem;
  background-color: #ffffffdc;
  margin-bottom: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.post-header {
  font-size: 1rem;
  color: #999;
  font-weight: bold;
  margin-bottom: 0.5rem;
  font-family: Georgia, serif;
}

.post-content {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  font-family: 'Bukhari Script', sans-serif;
  color: #a86a24;
}

.post-actions {
  display: flex;
  justify-content: flex-end;
}
</style>