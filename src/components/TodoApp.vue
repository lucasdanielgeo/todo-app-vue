<template>
  <div class="todo-app" :class="{ 'todo-app__blured': isModalOpen }">
    <h1>Todo App</h1>
    <button class="button__add-todo" @click="toggleModal">+ Add todo</button>
    <todo-items
      @delete-todo="deleteTodo"
      @complete-todo="completeTodo"
      @edit-todo="editTodo"
      :items="items"
    />
  </div>
  <todo-modal
    :is-modal-open="isModalOpen"
    v-if="isModalOpen"
    :class="{ modalbackgorund: isModalOpen }"
    :edit-todo-id="editTodoId"
  >
    <todo-input v-if="!editMode" @revalidate="revalidate" />
    <todo-edit
      v-else
      :items="items"
      :edit-todo="editMode"
      :edit-todo-id="editTodoID"
      @revalidate="revalidate"
      @close-modal="toggleModal"
    />
  </todo-modal>
</template>

<script>
import TodoInput from './TodoInput.vue'
import TodoItems from './TodoItems.vue'
import TodoModal from './TodoModal.vue'
import TodoEdit from './TodoEdit.vue'

export default {
  components: {
    TodoInput,
    TodoItems,
    TodoModal,
    TodoEdit,
  },
  name: 'TodoApp',

  props: {
    msg: String,
  },
  data() {
    return {
      items: [],
      isModalOpen: false,
      editMode: false,
      editTodoID: '',
    }
  },
  methods: {
    async completeTodo({ id, title, description, completed }) {
      const data = { title, description, completed: !completed }
      const itemToUpdate = this.items.find((item) => item.id === id)
      itemToUpdate.loading = true
      itemToUpdate.completed = !completed
      fetch(`https://vue-todo-tasks.herokuapp.com/api/tasks/${id}`, {
        method: 'PUT',
        body: JSON.stringify(data),
        headers: {
          'Content-Type': 'application/json',
        },
      }).then(this.revalidate.bind(this))
      console.log(completed)
    },

    async deleteTodo(item) {
      this.items = this.items.filter(($item) => item.id != $item.id)

      await fetch(`https://vue-todo-tasks.herokuapp.com/api/tasks/${item.id}`, {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json',
        },
      })
      await this.revalidate()
    },

    async revalidate() {
      const response = await fetch(
        'https://vue-todo-tasks.herokuapp.com/api/tasks',
      )
      const data = await response.json()
      this.items = data.map((item) => ({
        ...item,
        loading: false,
      }))
      this.isModalOpen = false
      this.editMode = false
    },
    toggleModal() {
      this.isModalOpen = !this.isModalOpen
    },
    editTodo(item) {
      this.toggleModal()
      this.editMode = true
      console.log(item.id)
      this.editTodoID = item.id
    },
  },
  async created() {
    const response = await fetch(
      'https://vue-todo-tasks.herokuapp.com/api/tasks',
    )
    const data = await response.json()
    this.items = data
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@media (max-width: 600px) {
  .todo-app {
    max-width: 90vw;
  }
}

.todo-app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 500px;
  background-color: #ffffff;
  padding: 25px;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.075);
  border-radius: 5px;
}
.todo-app__blured {
  filter: blur(2.5px);
}

h1 {
  font-weight: 600;
  margin-bottom: 25px;
  text-align: center;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.modal-background {
  display: flex;
}
</style>
