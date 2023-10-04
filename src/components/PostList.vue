<template>
  <div class="post_list" v-if="$props.posts.length > 0">
    <h3>Список постов</h3>
    <div class="search_area">
      <TextField
          place-holder-value="Поиск..."
          style="margin-left: 10px; margin-right: 10px; width: 300px"
          v-bind:value="this.searchValue"
          @input="this.searchValue = $event.target.value"
      />
      <Button
          class="search_btn"
          @click="$emit('search', this.searchValue)"
      >
        Найти
      </Button>
    </div>

    <transition-group name="post-list">
      <PostItem
          v-for="post in $props.posts"
          :post="post"
          :key="post.id"
          @remove="$emit('remove', post)"
          @prepare="$emit('prepare', post)"
      />
    </transition-group>
  </div>
  <div class="empty_list" v-else>
    <h3>Список постов пуст</h3>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem.vue";
import Button from "@/components/UI/Button.vue";

export default {
  components: {Button, PostItem},
  props: {
    posts: {
      type: Array,
      required: true
    },
  },
  data() {
    return {
      id: '',
      name: '',
      description: '',
      posts: [],
      searchValue: ''
    }
  },
  name: "PostList",
  methods: {},
}
</script>

<style scoped>

.search_area {
  display: flex;
}

.search_btn {
  padding: 5px;
  border-color: cornflowerblue;
  background: white;
  color: cornflowerblue;
  border-radius: 5px;
  transition: 0.4s;
  margin-left: 10px;
}

.search_btn:hover {
  transition: 0.4s;
  color: white;
  background: cornflowerblue;
}

.post_list {
  border: solid 2px #81C784;
  padding: 5px;
  border-radius: 4px;
  margin: 15px 10px;
}

.empty_list {
  border: solid 2px red;
  padding: 5px;
  border-radius: 4px;
  margin: 15px 10px;
  color: red;
}

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}

.post-list-enter-active,
.post-list-leave-active {
  transition: all 1s ease;
}

.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>