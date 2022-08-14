<template>
  <form @submit.prevent>
    <input type="text" class="input" placeholder="Title" v-model="post.title">
    <input type="text" class="input" placeholder="Description" v-model="post.body">
    <button type="submit" class="btn" v-on:click="createPost">New post</button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('createPost', this.post)
      this.post = {
        title: "",
        body: ""
      }
    }
  },
  data() {
    return {
      post: {
        id: "",
        title: "",
        body: ""
      }
    }
  }
}
</script>

<style scoped>
.input {
  background: none;
  border: 1px solid teal;
  padding: 15px 20px;
  margin-top: 15px;
}

.btn {
  background: none;
  border: 1px solid teal;
  padding: 15px 20px;
  align-self: flex-end;
  margin-top: 15px;
  color: teal;
}
</style>