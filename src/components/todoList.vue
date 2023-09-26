<template>
  <ul class="todo-main">
    <li v-for="(item, index) in todoList" :key="item.id">
      <el-checkbox
        v-model="item.isCompleted"
        @change="handleChange(item)"
      ></el-checkbox>
      <div class="input-container">
        <el-input
          v-model="item.task"
          placeholder="请输入任务名称"
          @blur="toLook(item)"
          @keyup.native.enter="toLook(item)"
          v-if="item.editable"
          :ref="index"
        ></el-input>
        <span
          v-else
          @click="toEdit(item, index)"
          :class="item.isCompleted ? 'completed' : ''"
          >{{ item.task }}</span
        >
      </div>
      <el-button
        v-if="!item.editable"
        type="danger"
        class="button"
        @click="handleDelete(item.id)"
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
    toEdit(item, index) {
      if (item.hasOwnProperty("editable")) {
        item.editable = true;
      } else {
        // 这里用$set是因为用普通方式增加的editable属性值不是响应式的
        this.$set(item, "editable", true);
      }
      // $nextTick是当dom渲染完后才会执行
      this.$nextTick(() => {
        this.$refs[index][0].focus();
      });
    },
    toLook(item) {
      if (item.hasOwnProperty("editable")) {
        item.editable = false;
      } else {
        this.$set(item, "editable", false);
      }
    },
    handleChange(item) {
      if (item.isCompleted) {
        this.$message({
          message: `恭喜您完成了${item.task}`,
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
  padding: 0px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

ul {
  margin: 10px 0 0 0;
}

li {
  height: 38px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ddd;
  padding: 10px;
}
li:nth-last-child(1) {
  border-bottom: none;
}
li .input-container {
  flex: 1;
  margin-left: 5px;
}
.completed {
  text-decoration: line-through;
  color: #d9d9d9;
}
li .button {
  display: none;
}
li:hover .button {
  display: block;
}
</style>
<style>
.el-checkbox__input.is-checked .el-checkbox__inner,
.el-checkbox__input.is-indeterminate .el-checkbox__inner {
  background-color: #d9d9d9;
  border-color: #d9d9d9;
}
.el-checkbox__input.is-checked + .el-checkbox__label {
  color: #d9d9d9;
}
.el-checkbox.is-bordered.is-checked {
  border-color: #d9d9d9;
}
.el-checkbox__input.is-focus .el-checkbox__inner {
  border-color: #d9d9d9;
}
</style>
