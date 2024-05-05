<template>
  <q-page class="row items-center justify-evenly">
    <number-inputs title="Input Type Number Demo" active></number-inputs>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import NumberInputs from 'components/NumberInputs.vue';

export default defineComponent({
  name: 'IndexPage',
  props: {},
  components: {
    NumberInputs,
  },

  setup() {
    return {};
  },
});
</script>
