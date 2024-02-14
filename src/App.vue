<template>
  <div id="app">
    <SuggestionList/>
  </div>
</template>

<script>
import SuggestionList from '@/components/SuggestionList.vue';

export default {
  components: {
    SuggestionList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
