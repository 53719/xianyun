<template>
  <div>
    <!-- 头部组件 -->
    <Header />
    <!-- 内容占位组件 -->
    <nuxt />
    <!-- 页脚组件 -->
    <Footer />
  </div>
</template>

<script>
import Header from "@/components/header";
import Footer from "@/components/footer";
export default {
  components: {
    Header,
    Footer
  }
};
</script>

<style lang="less">
</style>