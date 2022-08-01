<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "New Post",
      newPostParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
          this.newPostParams = "";
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>{{ message }}</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <button v-on:click="createPost">Create</button>
    </form>
  </div>
</template>
