<template>
  <div id="app">
    <todoInput @addTask="addTaskToList"></todoInput>
    <todoList
      v-show="undoList.length !== 0"
      :todoList="undoList"
      @deleteTodo="handleDelete"
    ></todoList>
    <completeHeader
      :isShowCompleted="isShowCompleted"
      @changeShowCompleted="changeShowCompleted"
    ></completeHeader>
    <todoList
      v-show="isShowCompleted"
      :todoList="completedList"
      @deleteTodo="handleDelete"
    ></todoList>
  </div>
</template>

<script>
import todoInput from "@/components/todoInput";
import todoList from "@/components/todoList";
import completeHeader from "@/components/completeHeader";
import { nanoid } from "nanoid";
import cloneDeep from "lodash/cloneDeep";
export default {
  name: "App",
  data() {
    return {
      todoList: JSON.parse(localStorage.getItem("todoList")) || [],
      isShowCompleted: true,
    };
  },
  components: {
    todoInput,
    todoList,
    completeHeader,
  },
  methods: {
    addTaskToList(taskName) {
      this.todoList.unshift({
        id: nanoid(),
        task: taskName,
        isCompleted: false,
      });
    },
    changeShowCompleted(isShowCompleted) {
      this.isShowCompleted = isShowCompleted;
    },
    handleDelete(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
    },
  },
  computed: {
    undoList() {
      return this.todoList.filter((item) => !item.isCompleted);
    },
    completedList() {
      return this.todoList.filter((item) => item.isCompleted);
    },
  },
  watch: {
    todoList: {
      deep: true,
      handler(todoList) {
        const myTodoList = cloneDeep(todoList);
        myTodoList.forEach((item) => {
          delete item.editable;
        });
        localStorage.setItem("todoList", JSON.stringify(myTodoList));
      },
    },
  },
};
</script>

<style>
body {
  max-width: 540px;
  min-width: 320px;
  margin: 0 auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 40px;
  padding: 0 8px;
}
li {
  list-style: none;
}
</style>
