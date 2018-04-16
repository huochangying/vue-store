<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="icon iconfont icon-31goumaichongzhi"></i>
        <div>收银</div>
      </li>
      <li>
        <i class="icon iconfont icon-dianpu"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="icon iconfont icon-hanbao"></i>
        <div>商品</div>
      </li>
      <li>
        <i class="icon iconfont icon-huiyuanqia"></i>
        <div>会员</div>
      </li>
      <li>
        <i class="icon iconfont icon-tongji"></i>
        <div>统计</div>
      </li>
      <li>
        <i class="icon iconfont icon-gongnengjianyi"></i>
        <div>设置</div>
      </li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: ""
    }
</script>

<style scoped>
  .left-nav{
    color: #fff;
    font-size: 10px;
    height: 100%;
    background: #1D8CE0;
    float: left;
    width:60px;
  }
  .iconfont{
    font-size: 24px;
  }
  .left-nav li{
    text-align: center;
    border-bottom: 1px solid #ddd;
    padding:10px;
    cursor: pointer;
  }
</style>
