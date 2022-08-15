<template>
  <div class="app">
    <default-dialog v-model:show="dialogStatus">
      <PostForm @createPost="createPost"></PostForm>
    </default-dialog>
    <default-button @click="openDialog">Create post</default-button>
    <PostList :posts="posts" @removePost="removePost" class="post-list" v-if="!isPostLoading"></PostList>
    <div v-else class="loader">Post loading...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import AuthorList from "@/components/AuthorList";
import AuthorForm from "@/components/AuthorForm";
import DefaultButton from "@/components/UI/DefaultButton";
import DefaultDialog from "@/components/UI/DefaultDialog";
import axios from 'axios';

export default {
  mounted() {
    this.getPosts();
  },
  data() {
    return {
      posts: [],
      dialogStatus: false,
      dialogAuthorStatus: false,
      authors: [
        {
          id: 1, name: "Ilya", surname: "Otinov"
        }
      ],
      isPostLoading: true,
    };
  },
  components: {
    DefaultDialog,
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
      this.authors.push(author);
      this.dialogAuthorStatus = false;
    },
    deleteAuthor(author) {
      this.authors = this.authors.filter(a => a.id !== author.id);
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    openDialog() {
      this.dialogStatus = true;
    },
    openAuthorDialog() {
      this.dialogAuthorStatus = true;
    },
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts?limit=10')
          .then(response => {
            this.posts = response.data
            this.isPostLoading = false;
          })
          .catch(exception => {
            console.log(exception.show);
          });

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
.post-list {
  margin-bottom: 20px;
}
.loader {
  display: flex;
  justify-content: center;
  background: rgb(0, 168, 255);
  padding: 15px;
  font-size: 30px;
  color: aliceblue;
}
</style>
