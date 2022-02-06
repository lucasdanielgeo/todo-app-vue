<template>
  <h1>Add new Todo</h1>
  <form class="input" @submit.prevent="handleSave">
    <label for="title">Title</label>
    <input type="text" v-model="title" />
    <label for="description">Description</label>
    <textarea v-model="description" />
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
  emits: ['ravalidate'],
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
    /**
     * It send a POST with title and description and emits an
     * event to revalidate todo list in parent component.
     */
    async handleSave() {
      const data = {
        title: this.title,
        description: this.description,
        completed: false,
      }
      this.title = ''
      this.description = ''

      await fetch('https://vue-todo-tasks.herokuapp.com/api/tasks', {
        method: 'POST',
        body: JSON.stringify(data),
        headers: {
          'Content-Type': 'application/json',
        },
      })
      this.$emit('revalidate')
    },

    /**
     * Changes state of isModalOpen to close modal
     */
    closeModal() {},
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-bottom: 0.5rem;
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
