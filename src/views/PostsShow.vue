<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id + ".json").then((response) => {
      this.post = response.data;
    });
  },
  methods: {
    destroyPost: function () {
      axios.delete("/posts/" + this.$route.params.id).then((response) => {
        console.log("Success!", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <div class="posts-show">
    <div class="container">
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
      <router-link to="/posts">Back to all Posts</router-link>
      |
      <router-link v-bind:to="`/posts/${post.id}/edit`">Edit this Post</router-link>
      |
      <button v-on:click="destroyPost()">Delete</button>
    </div>
  </div>
</template>
