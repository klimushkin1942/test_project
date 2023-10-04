<template>
  <div class="post">
    <div><strong>Название: </strong>{{ post.name }}</div>
    <div><strong>Описание: </strong>{{ post.description }}</div>
    <div class="post__btns">
      <Button
          class="delete_btn"
          @click="$emit('remove', post)"
      >
        Удалить
      </Button>
      <Button
          class="update_btn"
          @click="$emit('prepare', post)"
      >
        Обновить
      </Button>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  },
  name: "PostItem"
}
</script>

<style scoped>
.post {
  border: solid 2px #81C784;
  padding: 15px;
  border-radius: 4px;
  margin: 15px 10px;
}

.post:hover {
  color: #f5f4f4;
  background-color: #81C784;
  transition: 0.4s;
}

.post__btns {
  margin: 10px 0;
}

.delete_btn {
  padding: 5px;
  border-color: red;
  background: white;
  color: red;
  border-radius: 5px;
  transition: 0.4s;
}

.delete_btn:hover {
  transition: 0.4s;
  color: white;
  background: red;
}

.update_btn {
  padding: 5px;
  border-color: cornflowerblue;
  background: white;
  color: cornflowerblue;
  border-radius: 5px;
  transition: 0.4s;
  margin-left: 10px;
}

.update_btn:hover {
  transition: 0.4s;
  color: white;
  background: cornflowerblue;
}
</style>