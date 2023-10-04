<template>
  <div class="spinner"></div>
</template>

<script>
export default {
  name: "Loader"
}
</script>

<style scoped>
.spinner {
  border: dashed 5px #81C784;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  margin: 0 auto;
  animation: 1s linear 0s normal none infinite running loader;
}

@keyframes loader {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>