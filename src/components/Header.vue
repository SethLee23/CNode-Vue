<template>
  <div class="Header clearfix">
    <router-link :to="{name:'root',params:{page:1,limit:20,tab:'all'}}">
      <img src="../assets/cnodejs_light.svg" alt="logo" class="logo">
    </router-link>
    <!-- <ul>
      <li>
        <router-link :to="{name:'root',params:{page:1,limit:17}}">首页</router-link>
      </li> -->
      <!-- <li>
        <a href="#">新手入门</a>
      </li>
      <li>
        <a href="#">API</a>
      </li>
      <li>
        <a href="#">关于</a>
      </li>
      <li>
        <a href="#">注册</a>
      </li>
      <li>
        <a href="#">登陆</a>
      </li> -->
    </ul>
  </div>
</template>

<script>
export default {
  name: "Header"
};
</script>
<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.Header {
  /* border:1px solid red; */
  background: rgb(68, 68, 68);
}
.logo {
  width: 120px;
  padding-top: 9px;
  padding-bottom: 9px;
  margin-left: 13%;
}
ul {
  float: right;
  margin-right: 15.1%;
}
ul,
li {
  list-style-type: none;
  display: inline-block;
}

li > a {
  font-size: 13px;
  color: rgb(200, 200, 200);
  text-decoration: none;
}
li > a:hover {
  color: #fff;
}
li {
  line-height: 13px;
  padding-top: 17px;
  padding-bottom: 17px;
  margin-left: 25px;
}
.clearfix::after {
  display: block;
  clear: both;
  content: "";
}
</style>
