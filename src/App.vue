<template>
  <h1
    class="flex justify-center content-center mt-10 text-3xl font-bold text-slate-800"
  >
    My Todo List
  </h1>
  <Todo />
</template>

<script>
import "./index.css";
import Todo from "./components/Todo.vue";

export default {
  name: "App",
  components: {
    Todo,
  },
};
</script>
