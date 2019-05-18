<template>
  <div id="app">
<Header></Header>
<div class="main">
<router-view name="SliderBar"></router-view>
<router-view name="main"></router-view>
</div>
  </div>
</template>

<script>
import Header from './components/Header'
import PostList from './components/PostList'
import Article from './components/Article'
import UserInfo from './components/UserInfo'
export default {
  name: 'App',
  components:{
    Header,
    PostList,
    Article,
    UserInfo
  }
}
</script>

<style>
#app {
  overflow: auto;
  background: rgb(225,225,225);
}
.main{
  height: 100vh;
  width: 80%;
  margin: 0 auto;
}
</style>
