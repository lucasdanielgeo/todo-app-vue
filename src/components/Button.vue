<template>
  <button @click="$emit('clickEvent')" :style="`min-width: ${size}px`">
    {{ name }}
  </button>
</template>

<script>
export default {
  name: "Button",
  emits: ["click"],
  props: {
    name: String,
    buttonColor: String,
    size: {
      type: Number,
      default: 50,
    },
  },
};
</script>

<style>
button {
  border: none;
  height: 34px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px;
  color: white;
  background-color: #e0e0e0;
  font-weight: 500;
}
</style>
