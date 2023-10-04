<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "Button"
}
</script>

<style scoped>
.btn {
  padding: 5px;
  background: white;
  border-radius: 5px;
  transition: 0.4s;
}
.btn:hover {
  color: white;
  border-radius: 5px;
  transition: 0.4s;
}
</style>