<template>
  <div>
    <el-input
      placeholder="请输入任务名称，按下回车即可创建"
      v-model="taskName"
      @keyup.enter.native="add"
    >
      <template slot="prepend">+</template>
    </el-input>
  </div>
</template>

<script>
export default {
  name: "todoInput",
  data() {
    return {
      taskName: "",
    };
  },
  methods: {
    add() {
      if (!this.taskName.trim()) {
        return this.$message({
          message: "输入不能为空",
          type: "error",
          duration: 2000,
        });
      }
      this.$emit("addTask", this.taskName);
      this.taskName = "";
    },
  },
};
</script>

<style scoped></style>
