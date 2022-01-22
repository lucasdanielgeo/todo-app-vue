<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <TodoInput @save="handleSave" />
    <TodoItems :items="items" />
  </div>
</template>

<script>
import TodoInput from "./TodoInput.vue";
import TodoItems from "./TodoItems.vue";

export default {
  components: {
    TodoInput,
    TodoItems,
  },
  name: "TodoApp",

  props: {
    msg: String,
  },
  data() {
    return {
      items: [
        {
          name: "Criar componentes",
          done: false,
        },
        {
          name: "Criar componentes",
          done: true,
        },
      ],
    };
  },
  methods: {
    handleSave(description) {
      this.items.push({ name: description, done: false });
    },
  },
};
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
