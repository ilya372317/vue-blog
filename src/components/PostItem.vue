<template>
  <div class="post">
    <div>
      <div class="title"><strong>Название:</strong>{{ post.title }}</div>
      <div class="description"><strong>Описание:</strong>{{ post.body }}</div>
    </div>

    <div class="post-buttons">
      <default-button @click="removePost">Delete</default-button>
    </div>
  </div>
</template>

<script>
import DefaultButton from "@/components/UI/DefaultButton";

export default {
  name: "PostItem",
  components: {DefaultButton},
  props: {
    post: {
      type: Object,
      required: true,
    }
  },
  methods: {
    removePost() {
      this.$emit('removePost', this.post);
    }
  }
}
</script>

<style scoped>
.post {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  border: 1px solid teal;
  margin-top: 15px;
}
</style>