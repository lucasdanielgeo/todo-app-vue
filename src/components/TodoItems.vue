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
        class="button-icon button-icon__check"
      >
        <div class="button-icon button-icon__check">
          <refresh-icon v-if="item.loading" class="button-icon__spin" />
          <check-icon v-else />
        </div>
      </Button>
      <Button
        @click-event="$emit('delete-todo', item)"
        class="button-icon button-icon__delete"
      >
        <div class="button-icon button-icon__delete">
          <trash-icon />
        </div>
      </Button>
    </li>
  </ul>
</template>

<script>
import Button from './Button.vue'
import { CheckIcon, TrashIcon, RefreshIcon } from '@heroicons/vue/outline'
export default {
  components: {
    Button,
    TrashIcon,
    CheckIcon,
    RefreshIcon,
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

.button-icon {
  width: 20px;
}

.button-icon svg {
  width: 100%;
}

.button-icon__check:hover {
  background-color: rgb(0, 171, 102);
  color: white;
}
.button-icon__spin {
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.button-icon__delete:hover {
  background-color: rgb(221, 30, 5);
  color: white;
}
</style>
