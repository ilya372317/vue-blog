<template>
  <div class="app">
    <default-dialog v-model:show="dialogStatus">
      <PostForm @createPost="createPost"></PostForm>
    </default-dialog>
    <default-button @click="openDialog">Create post</default-button>
    <PostList :posts="posts" @removePost="removePost"></PostList>
    <AuthorForm @createAuthor="createAuthor"></AuthorForm>
    <AuthorList :authors="authors"></AuthorList>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import AuthorList from "@/components/AuthorList";
import AuthorForm from "@/components/AuthorForm";
import DefaultButton from "@/components/UI/DefaultButton";

export default {
  data() {
    return {
      posts: [
        {id: 1, title: "Why php is cool?", body: "because"},
        {id: 2, title: "Php 8 new features", body: "Enums it`s new meta"},
        {id: 3, title: "Best book about php", body: "Php-7 v podlinike is very impressive book."},
      ],
      dialogStatus: true,
      authors: [
        {
          id: 1, name: "Ilya", surname: "Otinov"
        }
      ]
    };
  },
  components: {
    DefaultButton,
    AuthorForm,
    PostList, PostForm, AuthorList
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogStatus = false;
    },
    createAuthor(author) {
      console.log(author);
      this.authors.push(author);
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    openDialog() {
      this.dialogStatus = true;
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


.app {
  padding: 15px;
  width: 1200px;
  margin: auto;
}

form {
  display: flex;
  flex-direction: column;
}


</style>
