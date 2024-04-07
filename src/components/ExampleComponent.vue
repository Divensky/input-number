<template>
  <div>
    <p>{{ title }}</p>

    <h2>Input number with validation</h2>
    <base-input-number></base-input-number>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import BaseInputNumber from './input/number/base-input-number.vue';

function useClickCount() {
  const clickCount = ref(0);
  function increment() {
    clickCount.value += 1;
    return clickCount.value;
  }

  return { clickCount, increment };
}

export default defineComponent({
  name: 'ExampleComponent',
  components: { BaseInputNumber },
  props: {
    title: {
      type: String,
      required: true,
    },
    active: {
      type: Boolean,
    },
  },

  setup() {
    return { ...useClickCount() };
  },
});
</script>
