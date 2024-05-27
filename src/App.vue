<template>
  <div id="app">
    <UsersSearch></UsersSearch>
    <ListPanel></ListPanel>
  </div>
</template>

<script>
import UsersSearch from "@/components/UsersSearch.vue";
import ListPanel from "@/components/ListPanel.vue";

export default {
  name: 'App',
  components: {
    ListPanel,
    UsersSearch,
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
