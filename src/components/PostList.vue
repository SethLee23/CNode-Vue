<template>
  <div class="PostList">
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif">
    </div>
    <div class="lists" v-else>
      <ul class="topbar">
        <span @click="changeTab">全部</span>
        <span @click="changeTab">精华</span>
        <span @click="changeTab">分享</span>
        <span @click="changeTab">问答</span>
        <span @click="changeTab">招聘</span>
        <span>关于</span>
      </ul>
      <ul class="titleList">
        <li v-for="list in this.lists">
          <!-- 动态绑定属性：src,注意key -->
          <img :src="list.author.avatar_url" alt>
          <span class="allCount">
            <span class="reply_count">{{list.reply_count}}</span>
            /{{list.visit_count}}
          </span>
          <span
            :class="[{good:(list.good==true||list.top==true)},{other:(list.good!=true&&list.top!=true)}]"
          >{{list|tabFormatter}}</span>
          <router-link
            :to="{
        name:'post_content',
        params:{
          id:list.id,
          name:list.author.loginname
        }}"
          >
            <span class="topic_title">{{list.title}}</span>
          </router-link>
          <span class="last_reply_at">{{list.last_reply_at|formatDate}}</span>
        </li>
      </ul>
    </div>
    <Pagination @handel="changePage"></Pagination>
  </div>
</template>

<script>
import Pagination from "./Pagination";
export default {
  name: "Header",
  data() {
    return {
      isLoading: false,
      lists: [],
      page: 1,
      tab: ""
    };
  },
  components: {
    Pagination
  },
  beforeMount: function() {
    this.isLoading = true;
    this.getPostListData();
  },
  methods: {
    getPostListData() {
      this.$http
        .get("https://cnodejs.org/api/v1/topics", {
          params: { page: this.page, limit: 17, tab: this.tab }
        })
        .then(res => {
          this.isLoading = false;
          this.lists = res.data.data;
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    changePage(value) {
      this.page = value;
      this.getPostListData();
    },
    changeTab(e) {
      console.log(e.currentTarget.innerText);
      switch (e.currentTarget.innerText) {
        case "全部":
          this.tab = "all";
          this.getPostListData();
          break;
        case "精华":
          this.tab = "good";
          this.getPostListData();
          break;
        case "分享":
          this.tab = "share";
          this.getPostListData();
          break;
        case "问答":
          this.tab = "ask";
          this.getPostListData();
          break;
        case "招聘":
          this.tab = "job";
          this.getPostListData();
          break;
      }
      return;
    }
  }
};
</script>
<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
li {
  list-style-type: none;
}
.loading {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.logo {
  display: inline-block;
  margin: 0 100px;
}
.PostList {
  max-width: 1094px;
  margin: 0 auto;
}
.titleList > li > img {
  width: 30px;
}
.PostList {
  margin-top: 14px;
}
.allCount {
  font-size: 12px;
  width: 70px;
  text-align: center;
}
.reply_count {
  color: rgb(158, 120, 192);
  font-size: 14px;
}
.good,
.other {
  font-size: 12px;
  padding: 2px 4px;
  border-radius: 3px;
  border-radius: 3px;
  color: #fff;
}
.good {
  background: #80bd01;
}
.other {
  background: #999999;
}
li {
  border-top: 1px solid rgb(225, 225, 225);
  display: flex;
  align-items: center;
  padding: 10px;
  position: relative;
  background: white;
}
li:hover {
  background: rgb(245, 245, 245);
}
.last_reply_at {
  position: absolute;
  right: 10px;
  color: #778087;
  font-size: 12px;
}

a:focus,
a:hover {
  color: #005580;
  text-decoration: underline;
}
a:active,
a:hover {
  outline: 0;
}
a {
  text-decoration: none;
  color: black;
  max-width: 70%;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  display: inline-block;
  font-size: 16px;
  line-height: 30px;
  margin-left: 5px;
  color: #333333;
}

a:hover {
  text-decoration: underline;
  color: #333333;
}
a:visited {
  color: #888888;
}
.topbar {
  height: 40px;
  background-color: #f5f5f5;
}

.topbar > span {
  font-size: 14px;
  color: #80bd01;
  line-height: 40px;
  margin: 0 10px;
  cursor: pointer;
  display: inline-block;
}

.toobar span:hover {
  color: #9e78c0;
}
</style>
