<template>
  <div>
    <div>{{ state.message }}</div>
    <Child
      :message="state.message"
      @change-message="changeMessage"
    />
  </div>
</template>

<script lang="ts">
import Child from '@/components/Child.vue';
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  name: 'Parent',
  components: {
    Child
  },
  setup() {
    const state = reactive({
      message: 'Hello'
    });

    const changeMessage = (message: string) => {
      state.message = message;
    };

    return {
      state,
      changeMessage
    };
  }
});
</script>