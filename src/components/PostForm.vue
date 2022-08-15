<template>
  <form @submit.prevent>
    <h2>Create post</h2>
    <default-input placeholder="Title" v-model="post.title"></default-input>
    <default-input placeholder="Description" v-model="post.body"></default-input>
    <default-button class="post-btn" @click="createPost">Create</default-button>
  </form>
</template>

<script>
import DefaultInput from "@/components/UI/DefaultInput";
export default {
  name: "PostForm",
  components: {DefaultInput},
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

.post-btn {
  align-self: flex-end;
  margin-top: 15px;
}
</style>