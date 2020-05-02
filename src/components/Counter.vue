<template>
  <div class="counter">
    <!-- <button @click="increment">
      count: {{ state.count }}, double: {{ state.double }}
    </button> -->

    <button @click="increment1">
      count: {{ state.counts[0] }} <!-- Vue 3.0のみ -->
    </button>
    <button @click="increment2">
      count: {{ state.counts[1] }} <!-- Vue 3.0のみ -->
    </button>
  </div>
</template>

<script lang="ts">
// import { defineComponent, reactive, computed } from 'vue';
import { defineComponent, reactive } from 'vue';

export default defineComponent ({
  name: 'Counter',
  setup() {
    // const state = reactive({
    //   count: 0,
    //   double: computed(() => state.count * 2),
    // });
    // const increment = () => {
    //   state.count++;
    // }

    // return {
    //   state,
    //   increment,
    // }

    const state = reactive({
      counts: [0, 0],
    });
    const increment1 = () => {
      state.counts[0]++;
    }
    const increment2 = () => {
      state.counts[1]++;
    }

    return {
      state,
      increment1,
      increment2,
    }
  }
});
</script>