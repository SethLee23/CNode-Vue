<template>

    <div class="Pagination">
      <ul class="full-rounded-blocks">
        <li>
          <span @click="changePage">上一页</span>
        </li>
        <li v-if="this.currentPage>1">
          <span class="normal" @click="changePage">back</span>
        </li>
        <li>
          <span
            v-for="page in pages"
            :class="[{currentPage: page === currentPage}]"
            @click="changePage(page)"
          >{{page}}</span>
        </li>
        <li>
          <span class="normal">...</span>
        </li>
        <li>
          <span class="normal" @click="changePage">下一页</span>
        </li>
      </ul>
    </div>
</template>

<script>
import $ from "jquery";
export default {
  name: "Pagination",
  data() {
    return {
      pages: [1, 2, 3, 4, 5],
      currentPage: ""
    };
  },
  methods: {
    changePage(page) {
      if (typeof page != "number") {
        console.log(page.target.innerText)
        switch (page.target.innerText) {
          case "上一页":
            $(".currentPage")
              .prev()
              .click()
            break;
          case "下一页":
            $(".currentPage")
              .next()
              .click()
            break;
          case "back":
            this.pages = [1, 2, 3, 4, 5]
            this.changePage(1)
            break;
          default:
            break;
        }
        return;
      }
      this.currentPage = page;
      if (page === this.pages[4]) {
        this.pages.splice(0, 1);
        this.pages.push(page + 1);
      } else if (page === this.pages[0] && page > 1) {
        this.pages.splice(4, 1);
        this.pages.unshift(page - 1);
      }
      this.$emit("handel", this.currentPage);
    }
  }
};
</script>

<style scoped>
span{
cursor: pointer;
}
@import url("https://fonts.googleapis.com/css?family=Lato:100,100i,300,300i,400,400i,700,700i,900,900i");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Lato", sans-serif;
  font-size: 14px;
  color: #999999;
  word-wrap: break-word;
}

ul,
li {
  list-style: none;
}
.Pagination {
  padding: 15px 0;
}

.Pagination ul {
  display: flex;
  flex-flow: row wrap;
}

.Pagination ul li {
  margin: 0 5px 0 0;
  text-align: center;
  align-items: center;
  position: relative;
  align-items: center;
  display: flex;
}


ul.full-rounded-blocks li {
  margin: 0px;
  background: #7aa11b;
}

.full-rounded-blocks li span,
.normal {
  display: block;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  color: white;
  background: #9bc11f;
  text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.2);
  border: 6px solid transparent;
  transition: 0.1s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.full-rounded-blocks li span:hover,
.full-rounded-blocks li.active a,
.activebtn {
  transform: scale(1.3);
  position: relative;
  color: #f3ff71;
  z-index: 2;
}
.currentPage {
  transform: scale(1.3);
  border: 3px solid #6a8f0f !important;
  position: relative;
  color: #f3ff71;
  z-index: 2;
}

.full-rounded-blocks li span:hover,
.currentPage {
  z-index: 3;
}

.full-rounded-blocks li:first-of-type span:hover,
.full-rounded-blocks li:last-of-type span:hover {
  transform: scale(1);
  border: 6px solid transparent;
}

.full-rounded-blocks li:first-of-type span,
.full-rounded-blocks li:last-of-type span {
  width: auto;
  padding: 6px 10px 5px;
  border-radius: 0;
  background: #7aa11b;
}

.full-rounded-blocks li:first-of-type,
.full-rounded-blocks li:first-of-type span {
  border-radius: 30px 0 0 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.full-rounded-blocks li:last-of-type,
.full-rounded-blocks li:last-of-type span {
  border-radius: 0 30px 30px 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
