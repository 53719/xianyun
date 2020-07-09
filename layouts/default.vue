<template>
  <div>
    <!-- 头部组件 -->
    <Header />
    <!-- 内容占位组件 -->
    <nuxt />
  </div>
</template>

<script>
import Header from "@/components/header";
export default {
  components: {
    Header
  }
};
</script>

<style lang="less">
</style>