<template>
  <div id="app">
    <Index msg="Vue 3.0 Beta" />
    <Counter />
    <Parent />
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUpdated, onUnmounted } from 'vue';
import Index from './components/Index.vue';
import Counter from './components/Counter.vue';
import Parent from './components/Parent.vue';

export default defineComponent({
  name: 'App',
  components: {
    Index,
    Counter,
    Parent,
  },
  setup() {
    // ライフサイクルメソッド
    onMounted(() => {
      console.log('描画しました');
    });
    onUpdated(() => {
      console.log('更新しました');
    });
  }
});
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
