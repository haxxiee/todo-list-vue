<script>
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

export default {
  setup() {
    const inputText = ref("");
    const todos = ref([]);

    function handleSubmit() {
      todos.value.unshift({
        id: uuidv4(),
        text: inputText.value,
        complete: false,
      });
      inputText.value = "";
    }

    function completeHandler(todo) {
      todo.complete = !todo.complete;
    }

    function deleteHandler(todo) {
      todos.value = todos.value.filter((el) => el.id !== todo.id);
    }

    return {
      todos,
      inputText,
      handleSubmit,
      completeHandler,
      deleteHandler,
    };
  },
};
</script>

<template>
  <form
    @submit.prevent="handleSubmit"
    class="flex justify-center content-center my-5"
  >
    <div class="flex items-center border-b border-teal-500 py-2">
      <input
        v-model="inputText"
        class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none transition duration-200"
        type="text"
        placeholder="Add Todo"
      />
      <button
        class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded"
        type="submit"
      >
        Add
      </button>
    </div>
  </form>

  <div
    v-for="todo in todos"
    :key="todo.id"
    class="flex justify-center items-center"
  >
    <div
      class="flex justify-between items-center my-3 py-4 border-2 border-teal-500 w-96 rounded-lg drop-shadow-2xl"
    >
      <div class="form-check flex">
        <input
          @click="completeHandler(todo)"
          class="form-check-input appearance-none h-5 w-5 border border-gray-300 rounded-sm bg-white checked:bg-teal-500 focus:outline-none transition duration-200 my-1 mx-3 align-top bg-no-repeat bg-center bg-contain float-left cursor-pointer"
          type="checkbox"
          value=""
        />
        <p :class="{ test: todo.complete }">
          {{ todo.text }}
        </p>
      </div>
      <button @click="deleteHandler(todo)" class="mr-4">
        <fa icon="x" />
      </button>
    </div>
  </div>
</template>

<style>
.test {
  text-decoration: line-through;
  opacity: 0.6;
}
</style>
