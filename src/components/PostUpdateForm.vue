<template>
  <form class="update_post" @submit.prevent>
    <h3>Изменение поста</h3>
    <div class="text-field">
      <label class="text-field__label" for="name">Название</label>
      <TextField
          v-bind:value="preparedFormData.name"
          @input="preparedFormData.name = $event.target.value"
          class="text-field__input"
          type="text"
          name="name"
          id="name"
          placeholder="Название"
      />
    </div>
    <div class="text-field">
      <label class="text-field__label" for="description">Описание</label>
      <TextField
          v-bind:value="preparedFormData.description"
          @input="preparedFormData.description = $event.target.value"
          class="text-field__input"
          type="text"
          name="description"
          id="description"
          placeholder="Описание"
      />
    </div>
    <Button
        class="update"
        @click="updatePost(this.post.id)"
    >
      Изменить
    </Button>
  </form>
</template>

<script>
import axios from "axios";
import {reactive, watch} from "vue";

export default {
  props: {
    post: {
      type: Object,
      required: true,
      default: () => ({})
    },
    fetchPosts: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      formData: {
        id: '',
        name: '',
        description: ''
      }
    }
  },
  name: "PostUpdateForm",
  methods: {
    updatePost(postId) {
      const updatedPost = {
        'name': this.preparedFormData.name,
        'description': this.preparedFormData.description
      }
      axios.put(`http://127.0.0.1:8000/api/posts/${postId}`, updatedPost)
          .then(response => {
            alert('Пост обновлен!')
          })
          .catch(error => {
            alert(`Ошибка: ${error}`)
          })
      this.preparedFormData.name = this.preparedFormData.description = '';
      this.fetchPosts();
    }
  },
  setup(props) {
    const preparedFormData = reactive({
      name: props.post.name,
      description: props.post.description
    })
    watch(() => props.post, (formData, oldPost) => {
      preparedFormData.name = formData.name;
      preparedFormData.description = formData.description;
    });

    return {
      preparedFormData
    };
  },

}
</script>

<style scoped>
.text-field {
  margin-bottom: 2rem;
}

.text-field__input {
  display: block;
  width: 100%;
  height: calc(2.25rem + 2px);
  padding: 0.375rem 0.75rem;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.text-field__label {
  display: block;
  margin-bottom: 0.25rem;
}

.update_post {
  border: solid 2px #81C784;
  padding: 5px;
  border-radius: 4px;
  margin: 15px 10px;
}

.update {
  color: #81C784;
  border-color: #81C784;
}

.update:hover {
  background: #81C784;
}
</style>