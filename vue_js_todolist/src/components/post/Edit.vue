<template>
<div>
      <h4 class="text-center mt-20">
       <small>
         <button class="btn btn-success" v-on:click="navigate()"> View All Posts </button>
       </small>
    </h4>
        <div class="col-md-12 form-wrapper">
          <h2> Edit Post </h2>
          <form id="edit-post-form" @submit.prevent="editPost">
            <div class="form-group col-md-12">
                <label for="title"> Title </label>
                <input type="text" id="title" v-model="title" name="title" class="form-control" placeholder="Enter title">
            </div>
            <div class="form-group col-md-12">
                <label for="description"> Description </label>
                <input type="text" id="description" v-model="description" name="description" class="form-control" placeholder="Enter Description">
            </div>
            <div class="form-group col-md-12">
                <label for="body"> Write Content </label>
                <textarea id="body" cols="30" rows="5" v-model="result.body" class="form-control"></textarea>
            </div>
            <div class="form-group col-md-12">
                <label for="author"> Author </label>
                <input type="text" id="author" v-model="author" name="author" class="form-control">
            </div>

            <div class="form-group col-md-4 pull-right">
                <button class="btn btn-success" type="submit"> Edit Post </button>
            </div>
          </form>
        </div>
    </div>
</template>

<script>
// import { server } from "../../utils/helper";
// import axios from "axios";
import router from "../../router";
import store from "../../../storage/index";

export default {
  data() {
    return {
      id: 0,
      post: {},
      title:'',
      body:'',
      author: '',
      description:'',
      date_posted:'',

    };
  },
  computed:{
    result(){
      var id = this.$route.params.id,
      result = store.getters.results[id];
      this.title = result.title;
      this.description = result.description;
      this.author = result.author;
      this.body = result.body;
      this.date_posted = result.date_posted;
      return result;
    }
  },
  methods: {
    editPost() {
      var result = {
        title: this.title,
        description: this.description,
        body: this.body,
        author: this.author,
        date_posted: this.date_posted,
        done:false
      }
      var total = {
        id:this.$route.params.id,
        result:result
      }
      store.dispatch('update',total);
      router.push({ name: "home" });
    },  
    navigate() {
      router.go(-1);
    }
  }
};
</script>

