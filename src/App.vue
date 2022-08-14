<template>
  <div class="app">
    <PostForm @createPost="createPost"></PostForm>
    <PostList :posts="posts"></PostList>
    <AuthorForm @createAuthor="createAuthor"></AuthorForm>
    <AuthorList :authors="authors"></AuthorList>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import AuthorList from "@/components/AuthorList";
import AuthorForm from "@/components/AuthorForm";

export default {
  data() {
    return {
      posts: [
        {id: 1, title: "Why php is cool?", body: "because"},
        {id: 2, title: "Php 8 new features", body: "Enums it`s new meta"},
        {id: 3, title: "Best book about php", body: "Php-7 v podlinike is very impressive book."},
      ],
      authors: [
        {
          id: 1, name: "Ilya", surname: "Otinov"
        }
      ]
    };
  },
  components: {
    AuthorForm,
    PostList, PostForm, AuthorList
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
    },
    createAuthor(author) {
      console.log(author);
      this.authors.push(author);
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
