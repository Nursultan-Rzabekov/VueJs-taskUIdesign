<template>
    <div>

      <div class="text-center">
        <h1>Nursultan Rzabekov</h1>
       <p>Task1-Vue.js </p>

       <div v-if="results.length === 0">
            <h2> No post found at the moment </h2>
        </div>
      </div>
        <div class="row"   >
           <div class="col-md-6"  v-for="(post,index) in results">
              <div class="card mb-4 shadow-sm">
                <div class="box card-body" :class="{done: post.done}" >
                   <h2 class="card-img-top">{{ post.title }}</h2>
                  <p class="card-text">{{ post.body }}</p>
                  <div class="d-flex justify-content-between align-items-center">
                    <div class="btn-group" style="margin-bottom: 20px;">
                      <router-link :to="{name: 'Post', params: {id: index}}" class="btn btn-sm btn-outline-secondary">View Post </router-link>
                       <router-link :to="{name: 'Edit', params: {id: index}}" class="btn btn-sm btn-outline-secondary">Edit Post </router-link>
                       <button class="btn btn-sm btn-outline-secondary" v-on:click="deletePost(index)">Delete Post</button>
                       <div class="box">
                        <button class="btn btn-sm btn-outline-secondary" @click='post.done = !post.done'>{{ (post.done) ? 'Unmark' : 'Done'  }}</button>
                        </div>
                    </div>
                  </div>

                  <div class="card-footer">
                    <small class="text-muted">Posted on: {{ post.date_posted}}</small><br/>
                    <small class="text-muted">by: {{post.author}}</small>
                  </div>
                   
                </div>
              </div>
            </div>
      </div>
    </div>
</template>

<script>
// @ is an alias to /src
//import { server } from "@/utils/helper";
//import axios from "axios";
import store from "../../storage/index";

export default {
  data() {
    return {
      done:true,
    };
  },
  computed:{
    results(){
       return (store.getters.results)
    }
  },
  // created() {
  //   this.fetchPosts();
  // },
  methods: {
    // fetchPosts() {
    //   axios
    //     .get(`${server.baseURL}/blog/posts`)
    //     .then(data => (this.posts = data.data));
    // },
    deletePost(id) {
      // axios.delete(`${server.baseURL}/blog/delete?postID=${id}`).then(data => {
      //   console.log(data);
      //   
      // });
      store.dispatch('delete',id); 
      window.location.reload();
    }
  }
};
</script>


<style>
            .box {
                
            }
            .box.done {
                 background-color: aquamarine;
            }
</style>

