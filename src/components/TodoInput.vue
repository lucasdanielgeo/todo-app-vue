<template>
  <form class="input" @submit.prevent="handleSubmit">
    <input type="text" v-model="description" />
    <Button name="Save" :size="105" style="background-color: #00ab66" />
  </form>
</template>

<script>
import Button from "./Button.vue";
export default {
  components: {
    Button,
  },
  name: "TodoInput",
  emits: ["save"],
  data() {
    return {
      description: "",
    };
  },
  methods: {
    handleSubmit() {
      this.description && this.$emit("save", this.description);
      this.description = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  width: 100%;
  margin-bottom: 0.5rem;
}

form.input {
  display: flex;
  gap: 0.5rem;
  width: 100%;
}

input {
  flex: 1;
}
</style>
