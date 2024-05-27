<script>
export default {
  name: "ListPanel",
  data() {
    return {
      listPanel: {
        userList: [],
        isFirstTimeTips: true,
        isLoading: false,
        errorMassage: "",
      },
    }
  },
  mounted() {
    this.$bus.$on('getUserList', (listObj) => {
      this.listPanel = {...this.listPanel, ...listObj}
    });
  }
}

</script>

<template>
  <div class="list-panel">
    <div class="tips" v-show="listPanel.isFirstTimeTips">欢迎使用,输入内容点击搜索查询</div>
    <div class="tips" v-show="listPanel.isLoading">加载内容中,请稍后...</div>
    <div class="tips" v-show="listPanel.errorMassage!==''">{{ listPanel.errorMassage }}</div>
    <ul>
      <li v-for="user of listPanel.userList" :key="user.id">
        <a :href="user.html_url" target="_blank">
          <img :src="user.avatar_url"/>
        </a>
        <span>{{ user.login }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.list-panel ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.list-panel li {
  list-style-type: none;
  width: 30%;
  margin-top: 200px;
}

.list-panel span {
  display: block;
  text-align: center;
  font-size: 1.5em;
}

.list-panel img {
  margin: 0 auto 0 auto;
  display: block;
  width: 300px;
  height: 300px;
}

.list-panel .tips {
  margin-top: 220px;
  text-align: center;
  background-color: white;
  font-size: 2em;
}
</style>