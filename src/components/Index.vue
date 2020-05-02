<template>
  <div class="index">
    <h1>{{ msg }}</h1>
    
    <!-- 従来の描画 -->
    <!-- <h2>{{ title }}</h2>
    <div>{{ message }}</div> -->

    <!-- reactive, ref使用 -->
    <h2>{{ state.title }}</h2>
    <div>{{ state.message }}</div>
    <div>{{ refMessage }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';

export default defineComponent ({
  name: 'Index',
  props: {
    msg: String,
  },
  // 従来のreactive
  // data() {
  //   return {
  //     title: 'Hello World',
  //     message: 'This is a Vue 3.0 - Beta',
  //   }
  // },

  // setup関数使用
  setup() { 
    const state = reactive ({
      title: 'Hello World',
      message: 'This is a Vue 3.0 - Beta',
    });
    
    const refMessage = ref('こんにちは');

    return {
      state,
      refMessage
    }
  }
});
</script>