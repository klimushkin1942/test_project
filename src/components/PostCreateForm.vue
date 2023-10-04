<template>
  <form class="create_post" @submit.prevent>
    <h3>Создание поста</h3>
    <div class="text-field">
      <label class="text-field__label" for="name">Название</label>
      <TextField
          v-model="post.name"
          type="text"
          placeholder="Название"
      />
    </div>
    <div class="text-field">
      <label class="text-field__label" for="description">Описание</label>
      <TextField
          v-model="post.description"
          type="text"
          placeholder="Описание"
      />
    </div>
    <Button
        class="add"
        @click="createPost"
    >
      Добавить
    </Button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        name: '',
        description: ''
      },
    }
  },
  name: "PostCreateForm",
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
        name: '',
        description: ''
      }
    },
  },
}
</script>

<style scoped>
.create_post {
  border: solid 2px #81C784;
  padding: 5px;
  border-radius: 4px;
  margin: 15px 10px;
}

.text-field {
  margin-bottom: 2rem;
}

.text-field__label {
  display: block;
  margin-bottom: 0.25rem;
}

.add {
  color: #81C784;
  border-color: #81C784;
}

.add:hover {
  background: #81C784;
}

</style>