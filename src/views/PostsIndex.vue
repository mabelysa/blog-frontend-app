<template>
  <div class="allposts">
    <h2>{{ message }}</h2>
    <div class="card-deck">
      <div class="card">
        Search by title:
        <input v-model="titleFilter" />
        <div
          v-for="post in filterBy(posts, titleFilter, 'title')"
          :key="post.id"
          v-bind:class="{ selected: post === currentPost }"
          v-on:click="currentPost = post"
        >
          <img class="card-img-top" v-bind:src="post.image" alt="Card image cap" />
          <div class="card-body">
            <h5 class="card-title">Title: {{ post.title }}</h5>
            <p class="card-text">
              <b>Body:</b>
              {{ post.body }}
            </p>
            <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
          </div>
        </div>
      </div>
    </div>

    <!-- <div v-for="post in posts" :key="post.id">
      <h2>Title: {{ post.title }}</h2>
      <p>
        <b>Body:</b>
        {{ post.body }}
      </p>
      <router-link v-bind:to="`/posts/${post.id}`">
        <img v-bind:src="post.image" alt="post.image" />
      </router-link>
    </div> -->
  </div>
</template>

<style>
.card {
  width: 75%;
}

.selected {
  color: white;
  background-color: deeppink;
  transition: background-color 1s ease;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  data: function () {
    return {
      message: "Here are the posts!",
      posts: [],
      currentPost: {},
      titleFilter: "",
    };
  },
  mixins: [Vue2Filters.mixin],
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts:", this.posts);
      });
    },
  },
};
</script>
