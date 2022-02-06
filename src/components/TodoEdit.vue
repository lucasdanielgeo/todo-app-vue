<template>
  <header>
    <h1>Update Todo</h1>
    <Button @click="$emit('closeModal')">
      <div class="button-icon">
        <arrow-left-icon />
      </div>
    </Button>
  </header>
  <form class="input" @submit.prevent="handleUpdate">
    <label for="title">Title</label>
    <input type="text" v-model="title" />
    <label for="description">Description</label>
    <textarea v-model="description" />
    <Button name="Update Todo" :size="105" :style="styleButton" />
  </form>
</template>

<script>
import Button from './Button.vue'
import { ArrowLeftIcon } from '@heroicons/vue/outline'

export default {
  components: {
    Button,
    ArrowLeftIcon,
  },
  props: ['edit-mode', 'items', 'edit-todo-id'],
  name: 'TodoInput',
  emits: ['ravalidate', 'close-modal'],
  data() {
    return {
      title: '',
      description: '',
      editTodo: null,
      styleButton: {
        backgroundColor: '#ff6600',
        color: 'white',
      },
    }
  },
  methods: {
    /**
     * Retrieve todo item data.
     */
    async retrieveTodoInfo() {
      const response = await fetch(
        `https://vue-todo-tasks.herokuapp.com/api/tasks/${editTodoID}`,
      )
      const data = await response.json()
      this.editTodo = data
      this.isModalOpen = false
    },

    /**
     * It send a POST with title and description and emits an
     * event to revalidate todo list in parent component.
     */
    async handleUpdate() {
      const data = {
        title: this.title,
        description: this.description,
        completed: false,
      }
      this.title = ''
      this.description = ''

      await fetch('https://vue-todo-tasks.herokuapp.com/api/tasks', {
        method: 'PUT',
        body: JSON.stringify(data),
        headers: {
          'Content-Type': 'application/json',
        },
      })
      this.$emit('revalidate')
    },
  },
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
}

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
  color: #ff6600;
}
</style>
