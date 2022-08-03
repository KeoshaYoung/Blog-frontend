<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Blog Posts",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts.json").then((response) => {
        this.posts = response.data;
        console.log("All Posts:", this.posts);
      });
    },
  },
};
</script>

<template>
  <h1>{{ message }}</h1>
  <div v-for="post in posts" v-bind:key="post.id">
    <router-link v-bind:to="`/posts/${post.id}`">
      <h3>{{ post.title }}</h3>
    </router-link>
    <img :src="post.image" alt="" />
    <p>
      {{ post.body }}
    </p>
  </div>
</template>
