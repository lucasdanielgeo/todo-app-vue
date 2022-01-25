<template>
  <ul>
    <h2>Todo List 😉</h2>
    <li v-for="item in reverseItems" :key="item.id">
      <input
        :class="{ done: item.completed }"
        class="todo-item"
        :value="item.title"
      />
      <Button
        @click-event="$emit('complete-todo', item)"
        :disabled="item.loading"
      >
        <span v-if="item.loading">Loading</span>
        <span v-else>Check</span>
      </Button>
      <Button @click-event="$emit('delete-todo', item)">
        <div class="icon">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
            />
          </svg>
        </div>
      </Button>
    </li>
  </ul>
</template>

<script>
import Button from './Button.vue'
export default {
  components: {
    Button,
  },
  name: 'TodoItem',
  props: ['items'],
  emits: ['complete-todo', 'delete-todo'],
  computed: {
    reverseItems() {
      return this.items.slice(0).reverse()
    },
  },
}
</script>

<style>
ul {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 0.5rem;
  margin-top: 20px;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

li {
  display: flex;
  align-items: center;
  width: 100%;
  gap: 0.5rem;
}

input.done {
  -webkit-text-decoration-line: line-through; /* Safari */
  text-decoration-line: line-through;
}
input.todo-item {
  border: none;
  background-color: rgb(236, 236, 236);
}

input {
  outline: none;
  height: 34px;
  width: 100%;
  border-radius: 5px;
  display: flex;
  padding-left: 15px;
  align-items: center;
}

.icon {
  width: 20px;
}

.icon svg {
  width: 100%;
}
</style>
