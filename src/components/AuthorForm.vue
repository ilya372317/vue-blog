<template>
  <h1>Create author</h1>
  <form @submit.prevent>
    <input type="text" class="input" placeholder="Name" v-model="author.name">
    <input type="text" class="input" placeholder="Surname" v-model="author.surname">
    <button type="submit" class="btn" v-on:click="createAuthor">make author</button>
  </form>
</template>

<script>
export default {
  name: "AuthorForm",
  data() {
    return {
      author: {
        name: "",
        surname: "",
      }
    }
  },
  methods: {
    createAuthor() {
      this.author.id = Date.now();
      this.$emit('createAuthor', this.author);
      this.author = {
        name: "",
        surname: ""
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  padding: 0;
  margin: 0;
}
.input {
  border: 1px solid teal;
  padding: 15px 20px;
  margin: 15px 0;
}
.btn {
  background: none;
  border: 1px solid teal;
  align-self: flex-end;
  padding: 10px 15px;
  color: teal;
}
</style>