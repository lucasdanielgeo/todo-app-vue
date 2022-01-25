<template>
  <form class="input" @submit.prevent="handleSubmit">
    <label for="title">Title</label> <input type="text" v-model="title" />
    <label for="description">Description</label>
    <textarea rows="4" v-model="description" />
    <Button name="+ Add Todo" :size="105" :style="styleButton" />
  </form>
</template>

<script>
import Button from './Button.vue'
export default {
  components: {
    Button,
  },
  name: 'TodoInput',
  emits: ['save'],
  data() {
    return {
      styleButton: {
        backgroundColor: '#00ab66',
        color: 'white',
      },
      title: '',
      description: '',
    }
  },
  methods: {
    handleSubmit() {
      this.title &&
        this.description &&
        this.$emit('save', this.title, this.description)
      this.title = ''
      this.description = ''
    },
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-bottom: 0.5rem;
}

form.input {
  gap: 1rem;
  width: 100%;
}

textarea {
  padding: 10px;
  resize: none;
  height: 74px;
}

label {
  font-weight: 600;
  font-size: 1.6rem;
}

input {
  flex: 1;
  min-height: 34px;
}
</style>
