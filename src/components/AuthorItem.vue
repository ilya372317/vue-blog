<template>
<div class="author">
      <div>
        <p><strong>Author name:</strong> {{ author.name }}</p>
        <p><strong>Author surname</strong> {{ author.surname }}</p>
      </div>
      <div class="author-buttons">
        <default-button v-on:click="deleteAuthor">Delete</default-button>
      </div>
    </div>
</template>

<script>
export default {
  name: "author-item",
  props: {
    author: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteAuthor() {
      this.$emit('deleteAuthor', this.author);
    }
  }
}
</script>

<style scoped>

</style>