<template>
    <div class="nav">
        <router-link to="/goods" class="nav-item goods">點餐</router-link>
        <router-link to="/ratings" class="nav-item ratings">評價</router-link>
        <router-link to="/seller" class="nav-item seller">商家</router-link>
    </div>
</template>

<script>
</script>

<style lang="scss" scoped>
.nav {
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  .nav-item {
    flex: 1;
    text-align: center;
    font-size: 13px;
    text-decoration: none;
    color: #666666;
  }
  &.active{
     color: #FFBB22; 
  }
}
</style>
