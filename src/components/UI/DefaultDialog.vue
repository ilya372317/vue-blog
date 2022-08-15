<template>
  <div class="dialog" v-if="show === true" @click="hideDialog">
    <div class="dialog_form" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "default-dialog",
  props: {
    show: {
      required: true,
      type: Boolean,
      default: true
    }
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0,0,0, 0.5);
  display: flex;
  justify-content: center;
  position: fixed;
}
.dialog_form {
  margin: auto;
  background-color: white;
  border-radius: 5% 5% 5% 5%;
  padding: 15px;
}
</style>