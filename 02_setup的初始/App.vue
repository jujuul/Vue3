<template>
  <div>哈哈</div>
  <h1>{{ number }}</h1>
</template>

<script lang="ts">
import { defineComponent } from "vue";

// 暴露出去一个定义好的组件
export default defineComponent({
  name: "App",
  // setup是组合API中第一个要使用的函数
  // setup() {
  //   const number = 10;
  //   return {
  //     number,
  //   };
  // },
});
</script>
