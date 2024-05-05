<template>
  <div class="q-mx-lg">
    <h1>{{ title }}</h1>
<p>Let's consider <pre class="text-accent">input type="number"</pre></p>
<p>When a user types non-numbers in the input field intended for numbers only, some browsers (such as Firefox) display the letters typed. However, internally they don't recognize the non-numbers. They record an empty strig when a user types non-numbers. Most of the browsers do not display an error message when a user types non-numbers into a number input.</p>
<p>This error message can be displayed in Quasar through the use of <strong>keyup</strong> and <strong>keydown</strong> events.</p>
<p>See what happens when you enter numbers and non-numbers in these inputs:</p>
    <h2>Input number with validation</h2>
    <base-input-number v-model="input" />
    <div>You entered the value: <strong>{{ inputDisplay }}</strong></div>

    <h2>Input number without validation</h2>
    <base-input-number v-model="input" :hide-errors="true"/>
    <p>You entered the value: <strong>{{ inputDisplay }}</strong></p>

  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';
import BaseInputNumber from './input/number/base-input-number.vue';

export default defineComponent({
  name: 'NumberInputs',
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
    const input = ref(null);
    const inputDisplay = computed(() => input.value === '' ? '(empty string)' : input.value )
    return {input, inputDisplay};
  },
});
</script>
