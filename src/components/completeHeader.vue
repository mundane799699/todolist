<template>
  <div @click="changeStatus" class="noselect cursor padding10">
    <span v-if="isShowCompleted"
      ><svg
        t="1695482635795"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="3442"
        width="16"
        height="16"
      >
        <path
          d="M512 714.666667c-8.533333 0-17.066667-2.133333-23.466667-8.533334l-341.333333-341.333333c-12.8-12.8-12.8-32 0-44.8 12.8-12.8 32-12.8 44.8 0l320 317.866667 317.866667-320c12.8-12.8 32-12.8 44.8 0 12.8 12.8 12.8 32 0 44.8L533.333333 704c-4.266667 8.533333-12.8 10.666667-21.333333 10.666667z"
          fill="#666666"
          p-id="3443"
        ></path></svg
    ></span>
    <span v-else
      ><svg
        t="1695482299791"
        class="icon"
        viewBox="0 0 1024 1024"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        p-id="9303"
        width="16"
        height="16"
      >
        <path
          d="M320 885.333333c-8.533333 0-17.066667-4.266667-23.466667-10.666666-12.8-12.8-10.666667-34.133333 2.133334-44.8L654.933333 512 298.666667 194.133333c-12.8-10.666667-14.933333-32-2.133334-44.8 10.666667-12.8 32-14.933333 44.8-2.133333l384 341.333333c6.4 6.4 10.666667 14.933333 10.666667 23.466667 0 8.533333-4.266667 17.066667-10.666667 23.466667l-384 341.333333c-6.4 6.4-12.8 8.533333-21.333333 8.533333z"
          fill="#666666"
          p-id="9304"
        ></path></svg
    ></span>
    已完成
  </div>
</template>

<script>
export default {
  name: "completeHeader",
  props: ["isShowCompleted"],
  data() {
    return {};
  },
  methods: {
    changeStatus() {
      this.$emit("changeShowCompleted", !this.isShowCompleted);
    },
  },
};
</script>

<style scoped>
.cursor {
  cursor: pointer;
}

.noselect {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.padding10 {
  padding: 10px 0 0 0;
}
</style>
