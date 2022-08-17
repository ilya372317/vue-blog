<template>
  <select v-model="modelValue" @change="changeSelect" class="select-default">
    <option value="" disabled>Select element</option>
    <option v-for="option in options" :value="option.value">{{ option.name }}</option>
  </select>
</template>

<script>
export default {
  name: "default-select",
  methods: {
    changeSelect(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  },
  props: {
    modelValue: {
      type: String,
      default() {
        return "";
      }
    },
    options: {
      type: Array,
      default() {
        return [];
      }
    }
  }
}
</script>

<style scoped>
.select-default {
  background: none;
  border: 1px solid teal;
  color: teal;
  padding: 10px 15px;
}
.select-default[aria-multiline] {
  background: red;
}
.select-default>option {
  background: none;
  border: 1px solid teal;
  font-size: 14px;
}
</style>