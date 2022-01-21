<template>
  <ul>
    <li v-for="(item, index) in items" :key="index">
      <span :class="item.done ? 'done' : ''"> {{ item.name }}</span>
      <Button @click="checkTodo" name="Check" />
      <Button @click="editTodo" name="Edit" />
    </li>
  </ul>
</template>

<script>
import Button from "./Button.vue";
export default {
  components: {
    Button,
  },
  name: "TodoItem",
  props: ["items"],
  methods: {
    editTodo() {},
    checkTodo() {},
  },
};
</script>

<style>
ul {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 0.5rem;
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

span {
  background-color: rgb(236, 236, 236);
  height: 34px;
  width: 100%;
  border-radius: 5px;
  display: flex;
  padding-left: 15px;
  align-items: center;
}
</style>
