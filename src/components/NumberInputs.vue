<template>
  <div class="q-mx-lg">
    <h1>{{ title }}</h1>
    <p>
      When users input non-numeric characters into a number-only field
      <span class="text-accent number-inputs__code">input type="number"</span>,
      browsers like Firefox may display them, but internally they're considered
      invalid and recorded as empty strings.
    </p>
    <p>
      Most browsers don't show error messages for this, potentially misleading
      users into thinking their input is valid when it's not.
    </p>
    <p>
      Since browsers convert non-numeric input to empty strings, traditional
      validation methods won't work. To address this, here is a demo of custom
      validation based on Quasar's <strong>keyup</strong> and
      <strong>keydown</strong> events.
    </p>
    <p>
      Let's see what happens when you enter numbers and non-numbers in these input
      fields:
    </p>
    <h2>Input number with validation</h2>
    <base-input-number v-model="input" />
    <div>
      Received value: <strong>{{ inputDisplay }}</strong>
    </div>

    <h2>Input number without validation</h2>
    <base-input-number v-model="input" :hide-errors="true" />
    <p>
      Received value: <strong>{{ inputDisplay }}</strong>
    </p>
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
    const inputDisplay = computed(() =>
      input.value === '' ? '(empty string)' : input.value
    );
    return { input, inputDisplay };
  },
});
</script>
<style scoped lang="scss">
.number-inputs__code {
  font-family: monospace;
}
</style>
