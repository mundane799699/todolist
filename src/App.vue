<template>
  <div id="app">
    <todoInput @addTask="addTaskToList"></todoInput>
    <todoList :todoList="undoList" @deleteTodo="deleteTodo"></todoList>
    <completeHeader
      :isShowCompleted="isShowCompleted"
      @changeShowCompleted="changeShowCompleted"
    ></completeHeader>
    <todoList
      :todoList="completedList"
      v-show="isShowCompleted"
      @deleteTodo="deleteTodo"
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
  computed: {
    completedList() {
      return this.todoList.filter((item) => item.isCompleted);
    },
    undoList() {
      return this.todoList.filter((item) => !item.isCompleted);
    },
  },
  methods: {
    addTaskToList(taskName) {
      this.todoList.unshift({
        id: nanoid(),
        task: taskName,
        isCompleted: false,
      });
    },
    changeShowCompleted(value) {
      this.isShowCompleted = value;
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
    },
  },
  components: {
    todoInput,
    todoList,
    completeHeader,
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
* {
  list-style: none;
}
</style>
