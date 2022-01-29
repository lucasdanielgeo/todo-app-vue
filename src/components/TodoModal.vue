<template>
  <div class="modal-background">
    <div class="modal-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoModal',
  props: ['isModalOpen'],
}
</script>

<style>
.modal-background {
  background-color: rgb(255, 254, 253);
  width: 350px;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.329);
  position: fixed;
  display: none;
  place-items: center;
}

.modal-content {
  width: 100%;
}
</style>
