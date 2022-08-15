<template>
<button class="btn">
  <slot></slot>
</button>
</template>

<script>
export default {
  name: "default-button"
}
</script>

<style scoped>
.btn {
  background: none;
  border: 1px solid teal;
  padding: 10px 15px;
  color: teal;
}
</style>