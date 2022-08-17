<template>
  <div class="app">
    <default-dialog v-model:show="dialogStatus">
      <PostForm @createPost="createPost"></PostForm>
    </default-dialog>
    <div class="post_buttons">
      <default-button @click="openDialog">Create post</default-button>
      <default-select v-model="selectedFilter" :options="filterOptions"></default-select>
      <default-input v-model="searchPost">Search</default-input>
    </div>
    <transition-group name="post-list">
      <PostList :posts="sortedAndSearchPosts" @removePost="removePost" v-if="!isPostLoading"></PostList>
      <div v-else class="loader">Post loading...</div>
    </transition-group>
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
import DefaultSelect from "@/components/UI/DefaultSelect";
import DefaultInput from "@/components/UI/DefaultInput";

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
      selectedFilter: "",
      filterOptions:
          [
            {
              name: "title",
              value: "title",
            },
            {
              name: "body",
              value: "body"
            },
            {
              name: "id",
              value: "id"
            }
          ],
      searchPost: "",
    };
  },
  components: {
    DefaultInput,
    DefaultSelect,
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
  },
  computed: {
    sortedPosts() {
      let newArray = this.posts;
      if (this.selectedFilter !== "") {
        if (this.selectedFilter !== "id") {


          newArray
              .sort(
                  (post1, post2) => {
                    return post1[this.selectedFilter].localeCompare(post2[this.selectedFilter]);
                  }
              );
        }
        if (this.selectedFilter === "id") {
          return newArray.sort(
              (post1, post2) => {
                if (post1[this.selectedFilter] < post2[this.selectedFilter]) {
                  return -1;
                }
                if (post1[this.selectedFilter] > post2[this.selectedFilter]) {
                  return 1;
                }
                if (post1[this.selectedFilter] === post2[this.selectedFilter]) {
                  return 0;
                }
              }
          );
        }
      }
      return newArray;
    },
    sortedAndSearchPosts() {
      return this.sortedPosts.filter(post => {
        return post.title.toLowerCase().includes(this.searchPost.toLowerCase());
      })
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

.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move {
  transition: transform 0.8s ease;
}
.loader {
  display: flex;
  justify-content: center;
  background: rgb(0, 168, 255);
  padding: 15px;
  font-size: 30px;
  color: aliceblue;
}
.post_buttons {
  display: flex;
  justify-content: space-between;
}
</style>
