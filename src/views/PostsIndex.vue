<script>
import axios from "axios";
import moment from "moment";
export default {
  data: function () {
    return {
      message: "Blog Posts",
      posts: [],
      currentPost: {},
      titleFilter: "",
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
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
    filterPosts: function () {
      return this.posts.filter((post) => {
        var lowerTitle = post.title.toLowerCase();
        var lowerTitleFilter = this.titleFilter.toLowerCase();
        return lowerTitle.includes(lowerTitleFilter);
      });
    },
  },
};
</script>

<template>
  <h1>{{ message }}</h1>
  Search by title:
  <input v-model="titleFilter" list="titles" type="text" />
  <datalist id="titles">
    <option v-for="post in posts" v-bind:key="post.id">{{ post.title }}</option>
  </datalist>
  <div v-for="post in filterPosts()" v-bind:key="post.id">
    <router-link v-bind:to="`/posts/${post.id}`">
      <h3>{{ post.title }}</h3>
    </router-link>
    <img :src="post.image" alt="" />
    <p>
      {{ post.body }}
      Updated: {{ relativeDate(post.updated_at) }}
    </p>
  </div>
</template>
