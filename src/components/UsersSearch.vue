<script>

import axios from "axios";

export default {
  name: 'UserSearch',
  data() {
    return {
      keyWord: "",
    }
  },
  methods: {
    getGithubUsers() {
      if (this.keyWord.trim()) {
        this.$bus.$emit('getUserList', {
          isFirstTimeTips: false,
          isLoading: true
        });
        axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(res => {
              this.$bus.$emit('getUserList', {
                userList: res.data.items,
                errorMassage: "",
                isFirstTimeTips: false,
                isLoading: false
              });
            },
            err => {
              this.$bus.$emit('getUserList', {userList: [], errorMassage: err.message, isLoading: false});
            });
      }
    }
  }
}
</script>

<template>
  <div class="users-search">
    <input class="search-box" type="text" placeholder="请输入关键词" autofocus v-model="keyWord"
           @keydown.enter="getGithubUsers">
    <input class="search-button" type="button" value="搜索" @click="getGithubUsers">
  </div>
</template>

<style scoped>
.users-search {
  height: 200px;
  background: linear-gradient(-30deg, #0a0c17, #10103a);
  text-align: center;
}

.users-search .search-box {
  border: none;
  height: 50px;
  width: 50vw;

  margin-top: 70px;

  vertical-align: bottom;

  background-color: white;
  color: white;
  font-size: 1.2em;
}

.users-search .search-button {
  border: none;
  background-color: rgb(29, 29, 110);
  width: 12vw;
  height: 50px;
  transition: 0.1s;

}

.users-search .search-button:hover {
  background-color: #414141;
  text-decoration: solid white 2px underline;

}
</style>