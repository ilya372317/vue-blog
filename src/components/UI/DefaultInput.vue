<template>
  <input type="{{ type }}" @input="createInput" :value="modelValue" class="input">
</template>

<script>
export default {
  name: "default-input",
  props: {
    type: {
      required: true,
      type: String
    },
    modelValue: {
      type: [String, Number],
      required: true
    }
  },
  methods: {
    createInput(event) {
      this.$emit("update:modelValue", event.target.value);
    }
  }
}
</script>

<style scoped>
.input {
  background: none;
  border: 1px solid teal;
  padding: 15px 20px;
  margin-top: 15px;
}
</style>