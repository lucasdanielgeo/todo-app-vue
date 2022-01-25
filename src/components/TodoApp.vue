<template>
  <div class="hello">
    <h1>{{ msg }} 💚</h1>
    <TodoInput @save="handleSave" />
    <TodoItems
      @delete-todo="deleteTodo"
      @complete-todo="completeTodo"
      :items="items"
    />
  </div>
</template>

<script>
import TodoInput from './TodoInput.vue'
import TodoItems from './TodoItems.vue'

export default {
  components: {
    TodoInput,
    TodoItems,
  },
  name: 'TodoApp',

  props: {
    msg: String,
  },
  data() {
    return {
      items: [],
    }
  },
  methods: {
    async handleSave(title, description) {
      const data = { title, description, completed: false }
      this.items.push(data)
      await fetch('https://vue-todo-tasks.herokuapp.com/api/tasks', {
        method: 'POST',
        body: JSON.stringify(data),
        headers: {
          'Content-Type': 'application/json',
        },
      })
      await this.revalidate()
    },

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
  .hello {
    max-width: 90vw;
  }
}

.hello {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 500px;
  background-color: #ffffff;
  padding: 25px;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.075);
  border-radius: 5px;
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
</style>
