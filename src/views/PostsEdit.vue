<template>
  <div class="editpost">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="currentPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="currentPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
      <button v-on:click="destroyPost()">Delete</button>
      <router-link to="/posts">Back to all Posts!</router-link>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post Info:", response.data);
      this.currentPostParams = response.data;
    });
  },
  methods: {
    updateRecipe: function () {
      axios.patch(`/posts/${this.$route.params.id}`, this.currentPostParams).then((response) => {
        console.log(response.data);
        this.$router.push(`/posts/${response.data.id}`);
      });
    },
    destroyPost: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log("Good job!", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
