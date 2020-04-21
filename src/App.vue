<template>
  <div id="app">
    <ArticleDetail></ArticleDetail>
  </div>
</template>

<script>
import ArticleDetail from './ArticleDetail.vue';

export default {
  name: 'App',
  components: {
    ArticleDetail,
  },
  data() {
    return {
    };
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background: #f5f5f5;
}
</style>
