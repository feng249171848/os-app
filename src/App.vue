<template>
  <div id="app">
    <!-- 头部 -->
    <app-header :poiInfo="poiInfo"></app-header>

    <!-- 导航 -->
    <app-nav :commentNum="commentNum"></app-nav>

    <!-- 内容 -->
    <!-- 保存组件状态避免重新渲染 -->
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import Header from './components/header/Header'
import Nav from './components/nav/Nav'

export default {
  name: 'App',
  components: {
    'app-header': Header,
    'app-nav': Nav
  },
  data(){
    return{
      poiInfo:{},
      commentNum:0
    }
  },
  created(){
    this.$axios("/api/goods/")
      .then(res => {
        if(res.data.code == 0){
          this.poiInfo = res.data.data.poi_info
        }
      })
    // 请求ratings
    this.$axios("/api/ratings/")
      .then(res => {
        if(res.data.code == 0){
          this.commentNum = res.data.data.comment_num
        }
      })  
  }
}
</script>

<style>

</style>
