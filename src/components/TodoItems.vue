<template>
  <ul>
    <li v-for="item in onlyUncompleted" :key="item.id">
      <span
        @dblclick="$emit('edit-todo', item)"
        :class="{ done: item.completed }"
        class="todo-item"
      >
        <div class="todo-title">{{ item.title }}:</div>
        <div class="todo-created-at">{{ item.created_at }}</div>
      </span>
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
    <li v-for="item in onlyCompleted" :key="item.id">
      <span
        @dblclick="$emit('edit-todo', item)"
        :class="{ done: item.completed }"
        class="todo-item"
      >
        <div class="todo-title">{{ item.title }}</div>
        <div class="todo-created-at">{{ item.created_at }}</div>
      </span>
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
  emits: ['complete-todo', 'delete-todo', 'edit-todo'],
  computed: {
    reverseItems() {
      return this.items.slice(0).reverse
    },
    onlyCompleted() {
      return this.items.slice(0).filter((item) => item.completed)
    },
    onlyUncompleted() {
      return this.items.slice(0).filter((item) => !item.completed)
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

span.done {
  -webkit-text-decoration-line: line-through; /* Safari */
  text-decoration-line: line-through;
}
span.todo-item {
  border: none;
  background-color: rgb(236, 236, 236);
}

span {
  display: flex;
  justify-content: space-between;
  outline: none;
  height: 34px;
  width: 100%;
  border-radius: 5px;
  display: flex;
  padding-left: 15px;
  padding-right: 15px;
  align-items: center;
}
.todo-title {
  font-weight: 600;
}
.todo-created-at {
  font-size: 0.9rem;
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
