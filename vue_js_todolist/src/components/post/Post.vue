<template>
    <div class="text-center">
        <div class="col-sm-12">
      <h4 style="margin-top: 30px;"><small><button class="btn btn-success" v-on:click="navigate()"> 
      View All Posts </button></small></h4>
      <hr>
      <h2>{{result.title}}</h2>
      <h5><span class="glyphicon glyphicon-time"></span> Post by {{result.author}}, {{result.date_posted}}.</h5>
      <p> {{ result.body }} </p>
  
    </div>
    </div>
</template>

<script>
import store from '../../../storage/index.js';

import router from "../../router";

export default {
  data() {
    return {
      title:'',
      body:'',
      author: '',
      description:'',
    }
  },
  computed:{
    result(){
      var id = this.$route.params.id;
      var result = store.getters.results[id];
      this.title = result.title;
      this.description = result.description;
      this.author = result.author;
      this.body = result.body;
      return result;
    }
  },
  methods: {
    navigate() {
      router.go(-1);
    }
  }
};
</script>

