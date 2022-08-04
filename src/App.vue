<script>
export default {
  data: function () {
    return {
      isLoggedIn: false,
      flashMessage: "You've successfully logged out!",
    };
  },
  methods: {
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.getItem("flashMessage");
      localStorage.removeItem("flashMessage");
    },
  },
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">Bloggr</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="/">Home</a>
          </li>
          <li class="nav-item">
            <a v-if="isLoggedIn" class="nav-link" href="/posts">Posts</a>
          </li>
          <li class="nav-item">
            <a v-if="isLoggedIn" class="nav-link" href="/posts/new">New Post</a>
          </li>
          <li class="nav-item">
            <a v-if="!isLoggedIn" class="nav-link" href="/signup">Signup</a>
          </li>
          <li class="nav-item">
            <a v-if="!isLoggedIn" class="nav-link" href="/login">Login</a>
          </li>
          <li class="nav-item">
            <a v-if="isLoggedIn" class="nav-link" href="/logout">Logout</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/contact">Contact Us</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div v-if="flashMessage" class="alert alert-info">
    {{ flashMessage }}
  </div>

  <router-view />
  <footer><h4>Follow Me</h4></footer>
</template>

<style>
h1 {
  font-family: monaco, Consolas, "Lucida Console", monospace;
  font-size: 24px;
  font-style: normal;
  font-variant: normal;
  font-weight: 700;
  line-height: 26.4px;
}
h3 {
  font-family: monaco, Consolas, "Lucida Console", monospace;
  font-size: 14px;
  font-style: normal;
  font-variant: normal;
  font-weight: 700;
  line-height: 15.4px;
}
p {
  font-family: monaco, Consolas, "Lucida Console", monospace;
  font-size: 14px;
  font-style: normal;
  font-variant: normal;
  font-weight: 400;
  line-height: 20px;
}
blockquote {
  font-family: monaco, Consolas, "Lucida Console", monospace;
  font-size: 21px;
  font-style: normal;
  font-variant: normal;
  font-weight: 400;
  line-height: 30px;
}
pre {
  font-family: monaco, Consolas, "Lucida Console", monospace;
  font-size: 13px;
  font-style: normal;
  font-variant: normal;
  font-weight: 400;
  line-height: 18.5714px;
}
body {
  background-image: url("./assets/ep_naturalwhite.webp");
}
</style>
