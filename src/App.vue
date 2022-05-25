<template>
  <div class="row border-top pt-4 mt-4 align-items-stretch">
      <div class="col-4 mb-4" v-for="(item,index) in service" :key="index">
        <div class="p-2 border h-100">
          <h1 v-html="item.title.rendered"></h1>
          <p v-html="item.content.rendered"></p>
        </div>
      </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'App',
  data() {
    return {
      content: "",
      genre: "",
      posts: [],
      service: [],
    };
  },
  mounted() {
    var vm = this;
    vm.url = "https://limylime.com/wp/wp-json/wp/v2";
    vm.get();
  },
  methods: {
    post() {
      var vm = this;
      axios
        .post(
          vm.url + "/service",
          vm.url + "/posts",
          {
            content: vm.content,
            author: 2,//consumerのユーザーID
            meta: {
              genre: vm.genre
            },
            status: "publish"
          },
        )
        .then(function() {
          vm.get();
        });
    },
    get() {
      var vm = this;
      axios.get(vm.url + "/service").then(function(response) {
        vm.service = response.data;
      });
      axios.get(vm.url + "/posts").then(function(response) {
        vm.posts = response.data;
      });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background-color: #2c3e50;
}
</style>
