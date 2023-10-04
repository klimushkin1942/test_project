<template>
  <div class="main__container">
    <h1>Страница с постами</h1>
    <Button @click="showDialog" class="create__btn">Создать пост</Button>
    <Dialog v-model:isOpen="flagDialog">
      <PostCreateForm
          @create="createPost"
      />
    </Dialog>
    <PostUpdateForm
        :post="this.post"
        :fetchPosts="fetchPosts"
    />
    <PostList
        :posts="this.posts"
        @remove="removePost"
        @prepare="preparePost"
        @search="searchPost"
        v-if="!isLoading"
    />
    <Loader v-else/>
  </div>
</template>

<script>
import axios from "axios";
import PostCreateForm from "@/components/PostCreateForm.vue";
import PostUpdateForm from "@/components/PostUpdateForm.vue";
import PostList from "@/components/PostList.vue";
import PostItem from "@/components/PostItem.vue";
import TextField from "@/components/UI/TextField.vue";

export default {
  components: {
    TextField,
    PostCreateForm,
    PostUpdateForm,
    PostList,
    PostItem,
  },
  data() {
    return {
      post: {
        id: '',
        name: '',
        description: ''
      },
      searchValue: '',
      posts: [],
      flagDialog: false,
      isLoading: false,
    }
  },
  name: "App",
  mounted() {
    this.fetchPosts();
  },
  methods: {
    preparePost(post) {
      this.post = post;
    },
    async createPost(post) {
      this.flagDialog = false;
      axios.post('http://127.0.0.1:8000/api/posts', post)
          .then(response => {
            alert('Пост успешно добавлен!');
          })
          .catch(error => {
            alert(`Ошибка ${error}`);
          })
      this.fetchPosts();
    },
    async removePost(post) {
      axios.delete(`http://127.0.0.1:8000/api/posts/${post.id}`)
          .then(response => {
            alert('Пост успешно удален!');
          })
          .catch(error => {
            alert(`Ошибка ${error}`);
          })
      this.fetchPosts();
    },
    async searchPost(searchValue) {
      axios.get('http://127.0.0.1:8000/api/search-posts', {
        params: {
          'name': searchValue,
          'limit': 5,
          'offset': 1,
        }
      })
          .then(response => {
            this.posts = response.data
          })
          .catch(error => {
            alert(`Error: ${error}`)
          })
    },
    showDialog() {
      this.flagDialog = true;
    },
    async fetchPosts() {
      this.isLoading = true;
      setTimeout(async () => {
        axios.get('http://127.0.0.1:8000/api/posts', {
          params: {
            limit: 3,
            offset: 1,
          }
        })
            .then(response => {
              this.posts = response.data
            })
            .catch(error => {
              alert(`Ошибка ${error}`)
            })
            .finally(() => {
              this.isLoading = false;
            })
      }, 1000);
    },
  }
}
</script>

<style>


* {
  margin: 0;
  padding: 0;
  font-family: Monaco;
  box-sizing: border-box;
}

.main__container {
  border: solid 2px #81C784;
  padding: 5px;
  border-radius: 4px;
  margin: 15px 10px;
}

.main__container .create__btn {
  color: #81C784;
  border-color: #81C784;
}

.main__container .create__btn:hover {
  background-color: #81C784;
}

</style>