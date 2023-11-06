<template>
 <div v-if="$route.path!='/info' && $route.path!='/zhuce' && $route.path!='/dengLu'">
  <van-tabbar  route active-color="#63a48e">
    <van-tabbar-item replace to="/" icon="home-o">首页</van-tabbar-item>
    <van-tabbar-item replace to="/about" icon="search">分类</van-tabbar-item>
    <van-tabbar-item replace to="/search" icon="cart-o">购物车</van-tabbar-item>
    <van-tabbar-item replace to="/my" icon="user-o">我的</van-tabbar-item>
  </van-tabbar>
 </div>
  <router-view />
</template>

<script setup lang="ts">
const path = ["/info", "/zhuce", "/denglu"];
</script>


<style lang="scss" >
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
li {
  list-style: none;
}
</style>


