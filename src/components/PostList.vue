<template>
  <div class="post" v-for="post in posts">
    <div class="title"><strong>Название:</strong>{{ post.title }}</div>
    <div class="description"><strong>Описание:</strong>{{ post.body }}</div>
  </div>
</template>

<script>
export default {
  name: "PostForm",
  props: {
    posts: {
      required: true,
      type: Array,
    }
  }
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: 1px solid teal;
  margin-top: 15px;
}
</style>