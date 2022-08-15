<template>
  <div v-if="posts.length > 0">
    <post-item v-for="post in posts" :post="post" :key="post.id" @removePost="removePost"/>
  </div>
  <div v-else>
    <h2 class="danger-alert">Список пользователей пуст!</h2>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostForm",
  components: {PostItem},
  props: {
    posts: {
      required: true,
      type: Array,
    }
  },
  methods: {
    removePost(post) {
      this.$emit('removePost', post)
    }
  }
}
</script>

<style scoped>
.danger-alert {
  color: crimson;
  font-size: 22px;
  font-style: italic;
}
</style>