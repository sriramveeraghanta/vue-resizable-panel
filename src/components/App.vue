<template>
  <div class="vue-split-panel-container clearfix" >
    <h1>Hello</h1>
  </div>
</template>

<script>
import SplitPane from 'components/App.vue'
export default {
  name: 'app',
  components: { SplitPane }
}
</script>

<style scoped>
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
.vue-split-panel-container {
  height: 100%;
  position: relative;
}
</style>