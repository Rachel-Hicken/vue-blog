<template>
<div id="app">
  <h1>Bob Loblaw's Law Blog</h1>
  <button @click='switcheroo'>Switcheroo</button>
  <section v-if='showForm'>
    <h3>Create new blog post:</h3>
    <form @submit.prevent='submitNewPost'>
      <textarea v-model='newPost' cols="30" rows="10"></textarea><br>
      Author: <input type="text" v-model='author'><br>
      <button>Submit new post</button> 
      <!-- by default the type of all buttons are submit -->
    </form>
  </section>
  <section v-else>
    <h3>List of blog posts:</h3>
    <list :posts='posts' :removePost='removePost'></list>
  </section>
</div>
</template>
<script>
import List from './components/List.vue';
export default {
  components: {
    list: List
  },
  //this is where import axios from 'axios' would go
  created(){
    console.log('created')
  },
  mounted(){
    console.log('mounted')
  },
  beforeMount(){
    console.log('beforeMount')
  },
  data(){
    return {
      newPost: '', 
      author: '', 
      posts: [], 
      id: 0, 
      showForm: true
    }
  }, 
  methods: {
    submitNewPost(){
     this.id ++;
     let newPost = {
       id: this.id,
       content: this.newPost, 
       author: this.author, 
       timeStamp: new Date()
     }
     this.posts.push(newPost);
     this.newPost = '';
     this.author = '';
     this.switcheroo();//or this.showForm: !this.showForm
    }, 
    switcheroo(){
      this.showForm = !this.showForm
    }, 
    removePost(id){
      this.posts = this.posts.filter(post=>{
        return  post.id !== id
      })
    }
  }
}
</script>
<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
