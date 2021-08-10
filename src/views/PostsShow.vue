<template>
  <div class="showpost">
    <div class="container">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
      <p><img v-bind:src="post.image" alt="post.image" /></p>
      <li v-if="$parent.getUserId() == post.user_id">
        <router-link v-bind:to="`/posts/${post.id}/edit`"><button>Edit Post</button></router-link>
      </li>

      <router-link to="/posts">Back to all Posts!</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
};
</script>
