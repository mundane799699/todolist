<template>
  <ul class="todo-main">
    <li v-for="item in todoList" :key="item.id">
      <el-checkbox
        v-model="item.isCompleted"
        @change="checkedChange(item)"
      ></el-checkbox>
      <div class="input-container">
        <el-input
          v-model="item.task"
          placeholder="请输入任务名称"
          @blur="toLook(item)"
          @keyup.native.enter="item.editable = false"
          v-if="item.editable"
          :ref="item.id"
        ></el-input>
        <span
          :class="item.isCompleted ? 'delete' : ''"
          v-else
          @click="toEdit(item)"
          >{{ item.task }}</span
        >
      </div>
      <el-button class="button" type="danger" @click="handleDelete(item.id)"
        >删除</el-button
      >
    </li>
  </ul>
</template>

<script>
export default {
  name: "todoList",
  props: ["todoList"],
  methods: {
    handleDelete(id) {
      this.$emit("deleteTodo", id);
    },
    toEdit(item) {
      this.$set(item, "editable", true);
      this.$nextTick(() => {
        console.log(this.$refs);
        console.log(this.$refs[item.id]);
        this.$refs[item.id][0].focus();
      });
    },
    toLook(item) {
      item.editable = false;
    },
    checkedChange(item) {
      if (item.isCompleted) {
        this.$message({
          message: `恭喜你，完成了${item.task}`,
          type: "success",
          duration: 2000,
        });
      }
    },
  },
};
</script>

<style scoped>
.todo-main {
  width: 500px;
  margin: 0 auto;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

li {
  height: 38px;
  line-height: 38px;
  padding: 10px 10px;
  border-bottom: 1px solid #ddd;
  display: flex;
}

li .input-container {
  flex-grow: 1;
  margin-left: 5px;
}

.delete {
  text-decoration: line-through;
  color: #d9d9d9;
}

li .button {
  float: right;
  display: none;
}

li:hover .button {
  display: block;
}
</style>
<style>
.el-checkbox__input.is-checked .el-checkbox__inner,
.el-checkbox__input.is-indeterminate .el-checkbox__inner {
  border-color: #d9d9d9 !important;
  background-color: #d9d9d9 !important;
}
.el-checkbox__input.is-focus .el-checkbox__inner {
  border-color: #d9d9d9 !important;
}
.el-checkbox__input.is-checked + .el-checkbox__label {
  color: #d9d9d9 !important;
}
</style>