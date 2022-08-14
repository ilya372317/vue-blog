<template>
  <div class="author-list">
    <h1>Author List</h1>
    <div class="author" v-for="author in authors">
      <p><strong>Author name:</strong> {{ author.name }}</p>
      <p><strong>Author surname</strong> {{ author.surname }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "AuthorList",
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
  }
}
</script>

<style scoped>
.author {
  display: flex;
  justify-content: center;
  flex-direction: column;
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