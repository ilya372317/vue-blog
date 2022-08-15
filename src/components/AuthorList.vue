<template>
  <div class="author-list">
    <h1>Author List</h1>
    <author-item v-for="author in authors" :key="author.id" :author="author" @deleteAuthor="deleteAuthor"/>
  </div>
</template>

<script>
import AuthorItem from "@/components/AuthorItem";
export default {
  name: "AuthorList",
  components: {
    AuthorItem
  },
  props: {
    authors: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      author: {
        id: '',
        name: '',
        surname: ''
      }
    }
  },
  methods: {
    deleteAuthor(author) {
      this.$emit('deleteAuthor', author);
    }
  }
}
</script>

<style scoped>
.author {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  border: 1px solid teal;
  margin-top: 15px;

}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

p {
  margin: 3px;
}
</style>