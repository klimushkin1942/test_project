<template>
  <input
      :value="modelValue"
      :placeholder="placeHolderValue"
      @input="updateInput"
      class="text-field__input"
      type="text"
  >
</template>

<script>
export default {
  name: "TextField",
  props: {
    modelValue: [String, Number],
    placeHolderValue: String
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>
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
</style>