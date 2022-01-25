<template>
  <button
    @click="$emit('click-event')"
    :style="`min-width: ${size}px`"
    :disabled="disabled"
  >
    {{ name }}
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
  emits: ['click-event'],
  props: {
    name: String,
    buttonColor: String,
    disabled: Boolean,
    size: {
      type: Number,
      default: 50,
    },
  },
}
</script>

<style>
button {
  border: none;
  height: 34px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 12px;
  font-family: Archivo;
  background-color: #e0e0e0;
  color: rgb(75, 94, 95);
  font-weight: 600;
  display: grid;
  place-items: center;
  transition: opacity ease-in-out 200ms, transform ease-in-out 200ms;
}

button:disabled {
  opacity: 0.5;
  background-color: darkcyan;
}
button:hover {
  transform: scale(1.025);
}
</style>
